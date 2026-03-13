////////////////////////////////////////////////////////////
// PSEUDOCODE: EXISTENCE FRAMEWORKS, VERIFIERS, AND
// NON-CONTRADICTION CONDITIONS
////////////////////////////////////////////////////////////


//////////////////////////////
// 1. CORE IDEA
//////////////////////////////

// Any meaning of "there exists" is defined by a parameter bundle theta
// and a verifier V_theta.
//
// Master schema:
//
// Exists_theta(X)  <=>  there exists some evidence package e
//                       such that Verify(theta, e, X) == TRUE


//////////////////////////////
// 2. DATA STRUCTURES
//////////////////////////////

TYPE Theta:
    Kind            // element, term, morphism, section, strategy, function
    Scope           // here, world(w), some_world, all_worlds, some_model, all_models, local_cover
    EvidenceMode    // none, proof, program, trace, section_data, strategy_certificate
    Constraints     // list of constraints: computable, time<=k, definable, canonical, stable, unique, etc.

TYPE EvidencePackage:
    witness         // the inhabitant candidate
    context         // world / model / cover / domain / other scope-specific data
    certificate     // proof / program / trace / strategy / section data / etc.

TYPE ExistenceMeaning:
    theta: Theta
    verifier: function(theta, e, X) -> boolean

TYPE ComparisonResult:
    same_base_universe: boolean
    same_scope: boolean
    same_candidate_space: boolean
    verifier_A_implies_B: boolean
    verifier_B_implies_A: boolean
    equivalent: boolean
    constraints_compatible: boolean
    non_contradictory: boolean


//////////////////////////////
// 3. MASTER SCHEMA
//////////////////////////////

FUNCTION Exists(theta, X):
    FOR each evidence_package e in CandidateEvidenceSpace(theta, X):
        IF Verify(theta, e, X) == TRUE:
            RETURN TRUE
    RETURN FALSE


//////////////////////////////
// 4. BUILDING A MEANING OF EXISTENCE
//////////////////////////////

FUNCTION BuildExistenceMeaning(
    target_sentence,
    kind,
    scope,
    evidence_mode,
    constraints
):
    theta = Theta(
        Kind = kind,
        Scope = scope,
        EvidenceMode = evidence_mode,
        Constraints = constraints
    )

    meaning = ExistenceMeaning(
        theta = theta,
        verifier = Verify
    )

    RETURN meaning


//////////////////////////////
// 5. VERIFY(theta, e, X)
//////////////////////////////

FUNCTION Verify(theta, e, X):
    IF ScopeOK(theta.Scope, e, X) == FALSE:
        RETURN FALSE

    IF KindOK(theta.Kind, e, X) == FALSE:
        RETURN FALSE

    IF EvidenceOK(theta.EvidenceMode, e, X) == FALSE:
        RETURN FALSE

    IF ConstraintsOK(theta.Constraints, e, X) == FALSE:
        RETURN FALSE

    RETURN TRUE


//////////////////////////////
// 6. KIND CHECK
//////////////////////////////

FUNCTION KindOK(kind, e, X):
    SWITCH kind:

        CASE "element":
            // witness a must be an element of X
            RETURN IsElementOf(e.witness, X)

        CASE "term":
            // witness t must typecheck as X
            RETURN TypeChecksAs(e.witness, X)

        CASE "morphism":
            // certificate must contain morphism 1 -> X
            RETURN HasMorphismFromTerminalObject(e.certificate, X)

        CASE "section":
            // certificate must contain section s in X(U)
            RETURN HasValidSection(e.certificate, X, e.context)

        CASE "strategy":
            // certificate must be a winning strategy for X
            RETURN IsWinningStrategy(e.certificate, X)

        CASE "function":
            // certificate must contain function of required form
            RETURN HasRequiredFunction(e.certificate, X)

        DEFAULT:
            RETURN FALSE


//////////////////////////////
// 7. SCOPE CHECK
//////////////////////////////

FUNCTION ScopeOK(scope, e, X):
    SWITCH scope.type:

        CASE "here":
            RETURN TRUE

        CASE "world":
            // witness must exist in X(w)
            RETURN WitnessLivesInWorld(e.witness, X, scope.world)

        CASE "some_world":
            // certificate/context must include some world w
            RETURN ExistsWorldInContext(e.context)
               AND WitnessLivesInWorld(e.witness, X, e.context.world)

        CASE "all_worlds":
            // evidence must work uniformly for every world
            RETURN UniformAcrossAllWorlds(e, X)

        CASE "some_model":
            // certificate/context must include some model M
            RETURN ExistsModelInContext(e.context)
               AND WitnessLivesInModel(e.witness, X, e.context.model)

        CASE "all_models":
            // evidence must work uniformly over all models in class K
            RETURN UniformAcrossAllModels(e, X, scope.model_class)

        CASE "local_cover":
            // certificate/context must contain a cover and local witnesses
            RETURN HasLocalCover(e.context)
               AND HasWitnessesOnCover(e, X, e.context.cover)

        DEFAULT:
            RETURN FALSE


//////////////////////////////
// 8. EVIDENCE CHECK
//////////////////////////////

FUNCTION EvidenceOK(evidence_mode, e, X):
    SWITCH evidence_mode:

        CASE "none":
            RETURN TRUE

        CASE "proof":
            RETURN IsValidProofObject(e.certificate, e.witness, X)

        CASE "program":
            RETURN IsProgram(e.certificate)
               AND ProgramHalts(e.certificate)
               AND ProgramOutputsWitness(e.certificate, e.witness, X)

        CASE "trace":
            RETURN IsAcceptedVerifierTrace(e.certificate, e.witness, X)

        CASE "section_data":
            RETURN HasCoverData(e.certificate)
               AND HasCompatibilityData(e.certificate)

        CASE "strategy_certificate":
            RETURN ProvesWinningStrategy(e.certificate, X)

        DEFAULT:
            RETURN FALSE


//////////////////////////////
// 9. CONSTRAINT CHECK
//////////////////////////////

FUNCTION ConstraintsOK(constraints, e, X):
    FOR each constraint in constraints:
        IF CheckSingleConstraint(constraint, e, X) == FALSE:
            RETURN FALSE
    RETURN TRUE


FUNCTION CheckSingleConstraint(constraint, e, X):
    SWITCH constraint.type:

        CASE "computable":
            RETURN IsComputable(e.witness, e.certificate)

        CASE "time_bound":
            RETURN RunsWithinBound(e.certificate, constraint.k)

        CASE "space_bound":
            RETURN UsesAtMostSpace(e.certificate, constraint.k)

        CASE "description_length":
            RETURN DescriptionLength(e.witness, e.certificate) <= constraint.k

        CASE "proof_length":
            RETURN ProofLength(e.certificate) <= constraint.k

        CASE "definable":
            RETURN IsDefinable(e.witness, X, constraint.allow_parameters)

        CASE "canonical":
            RETURN IsCanonicalRepresentative(e.witness, X)

        CASE "unique":
            RETURN IsUniqueWitness(e.witness, X)

        CASE "stable":
            RETURN PersistsUnderAllowedExtensions(e.witness, X, constraint.extension_policy)

        DEFAULT:
            RETURN FALSE


//////////////////////////////
// 10. CANDIDATE EVIDENCE SPACE
//////////////////////////////

FUNCTION CandidateEvidenceSpace(theta, X):
    // Conceptual generator:
    // returns all evidence packages matching the shape imposed by theta
    //
    // The important idea:
    // - theta.Kind determines witness shape
    // - theta.Scope determines context shape
    // - theta.EvidenceMode determines certificate shape

    RETURN GenerateAllEvidencePackagesMatchingTheta(theta, X)


//////////////////////////////
// 11. EXAMPLE: STANDARD GAME SEMANTICS
//////////////////////////////

// Standard existential quantifier:
//   Exists x P(x)
// is true iff Verifier can choose some x making P(x) true.

FUNCTION StandardExistentialGameTruth(structure M, predicate P):
    FOR each a in Domain(M):
        IF P(a) == TRUE:
            RETURN TRUE   // Verifier has winning move
    RETURN FALSE


//////////////////////////////
// 12. EXAMPLE: DEFINABLE EXISTENCE
//////////////////////////////

// New quantifier: Exists_def x P(x)
// means:
//   there exists a definable element a in M such that P(a) holds

FUNCTION DefinableExistence(structure M, predicate P):
    FOR each a in Domain(M):
        IF IsDefinableInStructure(a, M) == TRUE
           AND P(a) == TRUE:
            RETURN TRUE
    RETURN FALSE


//////////////////////////////
// 13. WHY DIFFERENT EXISTENCE NOTIONS CAN DISAGREE
//////////////////////////////

FUNCTION ShowPossibleDisagreement(structure M, predicate P):
    usual_exists = StandardExistentialGameTruth(M, P)
    definable_exists = DefinableExistence(M, P)

    IF usual_exists == TRUE AND definable_exists == FALSE:
        RETURN "Usual existence and definable existence disagree"

    IF usual_exists == FALSE AND definable_exists == TRUE:
        RETURN "Unexpected case under ordinary interpretation; check definitions"

    RETURN "No disagreement in this case"


// Important:
// disagreement here does NOT imply inconsistency.
// It means the two quantifiers are not the same quantifier.


//////////////////////////////
// 14. MECHANICAL PROCEDURE FOR BUILDING ANY
//     TYPE OF EXISTENCE
//////////////////////////////

FUNCTION GenerateExistenceMeaning():
    // Step 1: write target meaning in one sentence
    target_sentence = WriteTargetMeaning()

    // Step 2: choose inhabitant kind
    kind = ChooseOne([
        "element",
        "term",
        "morphism",
        "section",
        "strategy",
        "function"
    ])

    // Step 3: choose scope
    scope = ChooseOne([
        "here",
        "world",
        "some_world",
        "all_worlds",
        "some_model",
        "all_models",
        "local_cover"
    ])

    // Step 4: choose evidence requirement
    evidence_mode = ChooseOne([
        "none",
        "proof",
        "program",
        "trace",
        "section_data",
        "strategy_certificate"
    ])

    // Step 5: choose admissibility constraints
    constraints = ChooseAnySubset([
        "computable",
        "time_bound",
        "space_bound",
        "description_length",
        "proof_length",
        "definable",
        "canonical",
        "unique",
        "stable"
    ])

    // Step 6: assemble theta
    theta = Theta(kind, scope, evidence_mode, constraints)

    // Step 7: meaning is defined by existence of valid evidence package
    meaning = BuildExistenceMeaning(
        target_sentence,
        kind,
        scope,
        evidence_mode,
        constraints
    )

    RETURN meaning


//////////////////////////////
// 15. WORKED MINI-EXAMPLES
//////////////////////////////

FUNCTION ExampleA_ClassicalNonemptiness(X):
    theta = Theta(
        Kind = "element",
        Scope = "here",
        EvidenceMode = "none",
        Constraints = []
    )
    RETURN Exists(theta, X)
// Equivalent reading: X is non-empty


FUNCTION ExampleB_ComputableInhabitance(X):
    theta = Theta(
        Kind = "element",
        Scope = "here",
        EvidenceMode = "program",
        Constraints = ["computable"]
    )
    RETURN Exists(theta, X)
// Equivalent reading: X has a computable element


FUNCTION ExampleC_GlobalPoint(X):
    theta = Theta(
        Kind = "morphism",
        Scope = "here",
        EvidenceMode = "none",
        Constraints = []
    )
    RETURN Exists(theta, X)
// Equivalent reading: X has a global point / global element


FUNCTION ExampleD_LocalExistence(X):
    theta = Theta(
        Kind = "section",
        Scope = "local_cover",
        EvidenceMode = "section_data",
        Constraints = []
    )
    RETURN Exists(theta, X)
// Equivalent reading: X is locally inhabited


FUNCTION ExampleE_ActualistWorldRelativeExistence(X, w):
    theta = Theta(
        Kind = "element",
        Scope = MakeWorldScope(w),
        EvidenceMode = "none",
        Constraints = []
    )
    RETURN Exists(theta, X)
// Equivalent reading: X is inhabited at world w


//////////////////////////////
// 16. COMPARING TWO EXISTENCE MEANINGS
//////////////////////////////

// Let:
//   Exists_A(X)  <=>  there exists e such that V_A(e, X)
//   Exists_B(X)  <=>  there exists e such that V_B(e, X)
//
// We want conditions under which A and B are not contradicting each other.

FUNCTION CompareExistenceMeanings(theta_A, theta_B):
    result = ComparisonResult()

    result.same_base_universe =
        SameInhabitantKind(theta_A.Kind, theta_B.Kind)

    result.same_scope =
        SameScopePolicy(theta_A.Scope, theta_B.Scope)

    result.same_candidate_space =
        SameCandidateEvidenceShape(theta_A, theta_B)

    result.verifier_A_implies_B =
        VerifierImplies(theta_A, theta_B)

    result.verifier_B_implies_A =
        VerifierImplies(theta_B, theta_A)

    result.equivalent =
        result.verifier_A_implies_B
        AND result.verifier_B_implies_A

    result.constraints_compatible =
        ConstraintsAreCompatible(theta_A.Constraints, theta_B.Constraints)

    result.non_contradictory =
        CheckNonContradiction(result)

    RETURN result


//////////////////////////////
// 17. NON-CONTRADICTION CONDITIONS
//////////////////////////////

FUNCTION CheckNonContradiction(result):
    // Condition 1: same base universe and scope
    IF result.same_base_universe == FALSE:
        RETURN FALSE

    IF result.same_scope == FALSE:
        RETURN FALSE

    // Condition 2: same candidate space
    IF result.same_candidate_space == FALSE:
        RETURN FALSE

    // Condition 3: verifier nesting
    IF NOT (
        result.verifier_A_implies_B
        OR result.verifier_B_implies_A
    ):
        RETURN FALSE

    // Condition 4: compatible constraints
    IF result.constraints_compatible == FALSE:
        RETURN FALSE

    RETURN TRUE


//////////////////////////////
// 18. LOGICAL CONSEQUENCES OF NESTING
//////////////////////////////

FUNCTION ConsequenceOfImplication(theta_A, theta_B, X):
    // If V_A => V_B over same evidence space,
    // then Exists_A(X) => Exists_B(X)

    IF VerifierImplies(theta_A, theta_B) == TRUE:
        IF Exists(theta_A, X) == TRUE:
            RETURN Exists(theta_B, X) == TRUE

    RETURN "No implication available"


FUNCTION ConsequenceOfEquivalence(theta_A, theta_B, X):
    // If V_A <=> V_B, then Exists_A(X) <=> Exists_B(X)

    IF VerifierImplies(theta_A, theta_B) == TRUE
       AND VerifierImplies(theta_B, theta_A) == TRUE:
        RETURN Exists(theta_A, X) == Exists(theta_B, X)

    RETURN "No equivalence available"


//////////////////////////////
// 19. AVOIDING DIRECT CONTRADICTIONS
//////////////////////////////

FUNCTION ConstraintsAreCompatible(constraints_A, constraints_B):
    // Avoid complementary witness requirements such as:
    //   A: witness has property C
    //   B: witness has property not-C
    //
    // Safe patterns:
    // - nested constraints
    // - overlapping compatible constraints
    // - one stronger than the other

    IF AreComplementaryInWitnessForcingSense(constraints_A, constraints_B):
        RETURN FALSE

    RETURN TRUE


//////////////////////////////
// 20. FAST PRACTICAL CHECKLIST
//////////////////////////////

FUNCTION FastTestForNonContradiction(theta_A, theta_B):
    IF SameInhabitantKind(theta_A.Kind, theta_B.Kind) == FALSE:
        RETURN "Potential disagreement: different inhabitant kinds"

    IF SameScopePolicy(theta_A.Scope, theta_B.Scope) == FALSE:
        RETURN "Potential disagreement: different scope"

    IF SameCandidateEvidenceShape(theta_A, theta_B) == FALSE:
        RETURN "Potential disagreement: different candidate space"

    IF NOT (
        VerifierImplies(theta_A, theta_B)
        OR VerifierImplies(theta_B, theta_A)
    ):
        RETURN "Potential disagreement: no verifier nesting"

    IF ConstraintsAreCompatible(theta_A.Constraints, theta_B.Constraints) == FALSE:
        RETURN "Potential disagreement: incompatible constraints"

    IF VerifierImplies(theta_A, theta_B)
       AND VerifierImplies(theta_B, theta_A):
        RETURN "Equivalent meanings"

    RETURN "Non-contradictory, but one meaning is stronger than the other"


//////////////////////////////
// 21. MAIN SUMMARY
//////////////////////////////

FUNCTION Main():
    // 1. Any existence meaning is built from theta
    meaning = GenerateExistenceMeaning()

    // 2. Existence holds iff some evidence package satisfies verifier
    //    Exists(theta, X) <=> exists e Verify(theta, e, X)

    // 3. Different notions of existence may disagree without inconsistency
    //    if they use different witness rules, scope rules, or constraints

    // 4. To keep two meanings non-contradictory:
    //    - same inhabitant kind
    //    - same scope
    //    - same candidate space
    //    - verifier nesting
    //    - compatible constraints

    RETURN "Framework complete"
