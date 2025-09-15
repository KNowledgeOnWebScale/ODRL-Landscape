# ODRL Landscape

This document is collaborative effort that attempts to collect all projects, tooling and implementations that work with the Open Digital Rights Language (ODRL).

## What is ODRL?

The [Open Digital Rights Language (ODRL) Information Model 2.2](https://www.w3.org/TR/odrl-model/) is a W3C Recommendation to express **usage control policies**.

ODRL policies define **who** can perform **which action** on **which resource**, and under **what conditions**. These policies are composed of one or more **rules**, which are based on **deontic concepts**:
- **Permission**: explicitly allows an action. (e.g. *"Alice may **read** Resource X on Monday, 15 September 2025, between 09:00 and 17:00."*)  
- **Prohibition**: explicitly forbids an action. (e.g. *"Alice is **not allowed** to write to Resource X."*)  
- **Obligation**: requires an action to be fulfilled before or during usage. (e.g. *"Alice must **pay 5 euros** in order to read Resource X."*)  

## Why this document matters?

Orignally, ODRL was originally designed for **Digital Rights Management (DRM)**, focusing on expressing rights and obligations for digital content. 
For the most recent version, the scope was thus mainly on expression: providing a common information model for representing such policies.

Since ~2020, organizations have started exploring ODRL for access and usage control **enforcement**.
This shift created a need for **software and tooling** capable of **evaluating** ODRL policies in operational environments. 
For example, projects like [Solid](https://solidproject.org/TR/protocol) considered ODRL for data usage control (see related github issues: [WAC-10](https://github.com/solid/web-access-control-spec/issues/10), [WAC-87](https://github.com/solid/web-access-control-spec/issues/87), [Solid-56](https://github.com/solid/specification/issues/56#issuecomment-872020854), [Authz](https://solid.github.io/authorization-panel/authorization-ucr/#conditional-time)), but these efforts stalled due to the lack of a formalized, systematic evaluation approach.
Dataspaces also mention to use ODRL as usage control policy language for enforcement (both Gaia-X and IDSA).

Recently, significant progress has been made toward formalizing ODRL semantics.
The [ODRL Formal Semantics Community Group](https://w3id.org/odrl-fs/) is working on **standardizing the inputs** required for policy evaluation, such as the state of the world, the evaluation request, and the policies themselves.
In parallel, they are defining the **expected outputs** through the [Compliance Report Model](https://w3id.org/force/compliance-report) and developing a formal semantics for ODRL to ensure consistent and **interoperable evaluations across different implementations**.
As of today (15 September 2025), these efforts are ongoing.
This document aims to provide an overview of existing tools, frameworks, and approaches for ODRL policy evaluation, helping practitioners and researchers navigate the current landscape and contribute to these standardization efforts.


## Why this document matters

Originally, the [Open Digital Rights Language (ODRL)](https://wwwfor **Digital Rights Management (DRM)**, focusing on expressing rights and obligations for digital content. This was also the primary scope during the standardization process of **ODRL 2.2**, which aimed to provide a common information model for representing such policies.

Since around **2020**, organizations have started exploring ODRL for **access and usage control enforcement** beyond DRM. This shift created a need for **software and tooling** capable of evaluating ODRL policies in operational environments. For example, projects like Solid have considered ODRL for data access control (see related [issues](https://github.com/solid/authorization-panel/issues)), but these efforts stalled due to the **lack of a formalized, systematic evaluation approach**.

Recently, significant progress has been made toward formalizing ODRL semantics. The ODRL Formal Semantics Community Group is working on:
- **Standardizing inputs** for policy evaluation (e.g., stateefining outputs** through the Compliance Report Model.
- Developing a **formal semantics** for ODRL to enable consistent and interoperable evaluations.

As of today (**15 September 2025**), these efforts are ongoing. This document aims to provide an **overview of existing tools, frameworks, and approaches** for ODRL policy evaluation, helping practitioners and researchers navigate the current landscape and contribute to these standardization efforts.


## ODRL Evaluators

An ODRL Evaluator is defined as follows by the [ODRL Information Model 2.2](https://www.w3.org/TR/odrl-model/) as

>  A system that determines whether the Rules of an ODRL Policy expression have meet their intended action performance.

Thus, in this overview, we have added all evaluators that we know of. 
The table has three columns
- Name: what is the project name, with a link to the source
- Context: contains what it does (capabilities), which software language is used to implement it. 
  - Future work should include: the input (apart from the policies) and the output (yes/no vs compliance report vs ...)
- Authors: the group that created it and (if possible) a contact person

| Name                                                                                                 | Context                                                                                                                                                                                                                                 | Authors                                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [ODRL Evaluator](https://w3id.org/force/evaluator)                                                   | An open implementation of an ODRL Evaluator that evaluates ODRL policies by generating Compliance Reports.<br> Written in Node.js and Notation3 (prolog evaluated); runs in the [browser](https://w3id.org/force/demo)                  | [KNoWS](https://knows.idlab.ugent.be/) for the [Solidlab](https://solidlab.be/) project <br/> maintainer: [Wout Slabbinck](mailto:wout.slabbinck@ugent.be) |
| [Open Digital Rights Enforcement (ODRE) Framework](https://github.com/ODRE-Framework/odre-framework) | An open implementation of an ODRL Evaluator in multiple languages. <br> there is [ODRE for Java](https://github.com/ODRE-Framework/odre-java) and [ODRE for Python](https://github.com/ODRE-Framework/odre-python)                      | [OEG](https://oeg.fi.upm.es/) from [UPM](https://www.upm.es/) <br> maintainer: Andrea Cimmino                                                              |
| [ODRL-PAP](https://github.com/wistefan/odrl-pap)                                                     | Evaluates ODRL policies by translating them to [Rego policies](https://www.openpolicyagent.org/docs/policy-language), which are then executed by the [Open Policy Agent (OPA)](https://www.openpolicyagent.org/).  <br> Written in Java | Created for the [DOME-marketplace](https://dome-marketplace.eu/about) project                                                                              |
| [Odrl-manager](https://github.com/Prometheus-X-association/odrl-manager)                             | A library designed to facilitate the interpretation and evaluation of ODRL (Open Digital Rights Language) policies in JSON format.     <br> written in Node.js                                                                          | Prometheus-X                                                                                                                                               |
| [MOSAICrOWN policy engine](https://github.com/mosaicrown/policy-engine)                              | Parses and evaluates MOSAICrOWN policies, which uses as basis ODRL, but adds purpose as a first class citizen at rule level.<br> Written in Python                                                                                      | Created for the [MOSAICrOWN](https://cordis.europa.eu/project/id/825333) project (H2020)                                                                   |
| [MYDATA Control Technologies](https://git.iese.fraunhofer.de/mydata)                                 | Transforms ODRL policies to the custom XML-based MYDATA policy and evaluates the latter <br> Written in Java                                                                                                                            | Fraunhofer                                                                                                                                                 |
| [Gaia-X Wizard (PDP) Policy Stepper](https://wizard.lab.gaia-x.eu/policyStepper)                     | [gitlab repo](https://gitlab.com/gaia-x/lab/gaia-x-onboarding-prototypes/gx-signing-tool); <mark>TODO:</mark> how does it work and in which language is it written                                                                      | Gaia-X <br> maintainer: Yassir Sellami                                                                                                                     |
| [Polival](https://codeberg.org/elbtech/Polival)                                                      | Policy and semantic web evaluation <br> Written in Rust and SPAQRL                                                                                                                                                                      | [Elbtech](https://elbtech.dev/) <br> maintainer: Richard Stoffels                                                                                          |


## Frameworks using ODRL

- [ODRL-Test-Suite](https://w3id.org/force/test-suite)
- [User-managed-access (UMA server)](https://github.com/SolidLabResearch/user-managed-access)
- [FORCE UI](https://w3id.org/force/demo)
- [FORCE specification suite](https://w3id.org/force)
- [Gaia-X Wizard](https://wizard.lab.gaia-x.eu/development)
- [odrl-evaluation-engine-testbed](https://gitlab.com/gaia-x/lab/policy-reasoning/odrl-toolbox/-/tree/main/odrl-evaluation-engine-testbed)
- [Eclipse Dataspace Connector (EDC)](https://github.com/eclipse-edc/Connector)
- [Solid Agent UCP demo](https://github.com/SolidLabResearch/Solid-Agent/tree/feat/sosy/documentation/ucp)


## Protocols that point to ODRL

- [Dataspace Protocol](https://eclipse-dataspace-protocol-base.github.io/DataspaceProtocol)
- [Eclipse Dataspace Decentralized Claims Protocol](https://eclipse-dataspace-dcp.github.io/decentralized-claims-protocol/)
- [Authorization for Data Spaces](https://spec.knows.idlab.ugent.be/A4DS/L1/latest/)

## ODRL utilities

- [MyData ODRL policy creator](https://odrl-pap.mydata-control.de/)
- [ODRL Shape validation](https://github.com/woutslabbinck/ODRL-shape)
- [ODRL Validation implementation](https://odrlapi.appspot.com/)
- [Deontic Policy Consistency Checker](https://knowledgeonwebscale.github.io/n3s-policy-consistency-checker/)
- [LLM4ODRL](https://github.com/Daham-Mustaf/LLM4ODRL)
- [ODRL2SHACL](https://github.com/paolo7/ODRL2SHACL)

