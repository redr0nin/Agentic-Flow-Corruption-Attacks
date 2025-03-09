# Agentic Flow Corruption (AFC) Attacks: Red Team Tactics for Subverting AI Security Agents

## Introduction

Agentic AI systems represent an evolution from static machine learning models to autonomous decision-making entities capable of perceiving their environment, reasoning about complex goals, and executing sequences of actions to achieve those goals. While these systems offer unprecedented capabilities for automation in cybersecurity, their autonomous nature introduces novel attack surfaces that traditional security models fail to address. This paper introduces and analyzes Agentic Flow Corruption (AFC) attacks—a class of adversarial techniques that exploit the decision-making pipelines of AI agents by manipulating the environmental data they consume, rather than attacking the underlying models directly.

In this paper, we provide several examples of case studies in which we've observed the ability to perform agentic flow corruption (AFC) attacks which are described in-depth. These represent merely a subset of a much larger attack surface, as the vulnerability landscape is infinitely expansive. Artificial Intelligence relies on dynamic behavior, thus, a lot of the prevention methodology will negatively affect the operating capacity of the AI model overall.

We tested these methods on real AI frameworks utilizing Agentic AI workers. Rather than focus on the specific frameworks in question, we set out to define some of the methodology to craft your own AFC attacks. The below case studies are real-life examples of some methods that we have used to red team the red teamers.

Keep in mind that some adaptations were made, for instance in the case study where we had access to a RAG server, this was a bit of whitebox for an NDA government entity, offered via a mutual partnership in which we'd assist in discovering vulnerabilities in exchange for the ability to allow the no-name disclosure of said methodology. We may have modified timestamps, usernames, data and/or script names, etc., per guidance. Additionally, we've heavily modified a lot of the output of sample data.

## Purpose and Significance

The purpose of this research is to demonstrate that automation via Agentic AI agents introduces significant security vulnerabilities when these systems are not properly monitored and supervised. Are organizations prepared for attackers to poison the underlying data streams and environmental context that these autonomous frameworks depend on for decision-making? Through our case studies, we've demonstrated that attackers can effectively poison the indirect operating system data or functional components that frameworks incorporate into their autonomous workflow.

If you're a security professional considering replacing manual red team consultants with fully automated red teaming tooling, you should carefully reconsider this approach. The fundamental challenge is that patching agentic AI behavior against these attacks often requires constraining the agent's dynamic decision-making capabilities, which undermines the core value proposition of AI-driven automation. Furthermore, the attack methodology we describe can broadly impact any agentic AI framework, as the techniques simply need to adapt to the specific workflow of the agent in question.

## Disclosure Scope and Limitations

We have deliberately chosen not to highlight specific vulnerable models in this disclosure for several reasons:

1. Most of the attack methodology described affects a broad spectrum of commercial products, and initiating a comprehensive disclosure and CVE process for potentially hundreds of products and variations would be impractical.

2. Vendors would likely argue that they cannot be held responsible if an attacker gains access to a workstation, server, or device, and that they cannot reasonably patch their agent's logic to anticipate every possible environmental manipulation. This position has technical merit, which is precisely what makes AFC attacks so dangerous as these methods become commonplace tactics for malware deployment and network pivoting.

3. The distinctive characteristic of AFC attacks is their diversity—there are countless attack paths, variations, and scenarios that can unfold. The fundamental insight is that attackers aren't poisoning the agent itself but rather the data streams and functional interfaces it interacts with, enabling a wide spectrum of sophisticated disruption techniques.

## Definition and Classification of AFC Attacks

AFC attacks represent a novel class of adversarial techniques distinct from traditional prompt injection, model poisoning, or direct LLM manipulation. Rather than compromising the integrity of the model's parameters or training data, AFC attacks exploit the agent's operational context by corrupting the data streams and environmental signals that inform the agent's decision-making process. This creates a side-channel vulnerability in the agent's reasoning pipeline, allowing attackers to indirectly manipulate the agent's behavior while preserving the integrity of its core AI components. The attack vector exists in the interface between the agent's perception systems and execution mechanisms, making it particularly challenging to detect and mitigate without constraining the agent's autonomous capabilities.

### Relationship to Existing Attack Taxonomies

Agentic Flow Corruption attacks do not compromise the integrity of the dataset or LLM model directly. They differ from established attacks because while they CAN be used to permanently modify, damage, or abuse components within the Agentic AI flow or local system, the attack can be characterized as a form of side-channel attack on the logic of the agentic processing pipeline.

For example, consider the techniques described in the MITRE ATLAS Matrix. One of the technique categories, [ML Supply Chain Compromise (AML.T0010)](https://atlas.mitre.org/techniques/AML.T0010) describes various ways that attackers can abuse the Model, Data, ML Software, or Hardware to gain control over the AI. In contrast, AFC attacks compromise AI systems by poisoning local components on the workstation, server, or device to manipulate the agentic AI's behavior—which can subsequently lead to full compromise of the model itself, depending on the attacker's objectives. This approach varies significantly from MITRE's classification, which focuses on direct modifications or poisoning of the AI system. In AFC attacks, we don't poison the AI directly; we poison the systems it operates on and evaluates, to subsequently exploit either the AI or the network it has access to.

### Attack Taxonomy

AFC attacks can be categorized into several distinct subtypes:

1. **Environmental Context Poisoning** - Manipulating the data sources that agents use to understand their operational environment
2. **Decision Pathway Manipulation** - Exploiting the logical flow of agent reasoning processes
3. **Guardrail Inversion Attacks** - Weaponizing safety mechanisms to induce harmful behavior
4. **Feedback Loop Corruption** - Poisoning the agent's learning and adaptation mechanisms
5. **Multi-stage Orchestration Hijacking** - Compromising the coordination between multiple agent components

## Theoretical Agentic System Architecture

To better understand the vulnerability surface for AFC attacks, we present a realistic theoretical architecture for an autonomous red team system. This architecture encompasses the key components that would be present in modern agentic security systems:

### Multi-Modal Autonomous Red Team (MART) Reference Architecture

The following architecture serves as a reference model for autonomous security assessment systems. We present this framework to establish common terminology for discussing the components targeted in AFC attacks. Each case study will reference how its specific implementation maps to this reference architecture.

```
1. Command and Control Layer:
   - Orchestration component for task distribution and scheduling
   - Coordination mechanisms for synchronizing actions
   - Reporting interfaces for human oversight

2. Intelligence Layer:
   - Reasoning system for strategy and decision-making
   - Knowledge components for storing and retrieving security information
   - Planning module for sequencing attack strategies

3. Execution Layer:
   - Tool integration for invoking security assessment utilities
   - Command execution for system interaction
   - Result processing for interpreting outputs

4. Safety and Compliance Layer:
   - Ethical guardrails for preventing harmful actions
   - Operational boundaries for limiting scope
   - Impact assessment for evaluating consequences
   - Logging framework for audit trails
```

This simplified reference architecture provides a consistent framework for analyzing different autonomous security systems. Each real-world implementation will have its own specific components that map to these general capabilities, often with varying levels of sophistication and integration.

This architecture represents a typical agentic system that would be vulnerable to the attacks described in our case studies. Each layer presents distinct attack surfaces for AFC techniques.

## Attack Summary

Threat actors can systematically compromise autonomous systems through multiple technical vectors that align with the MART reference architecture layers:

1. **Decision Flow Hijacking**: Manipulating the agent's reasoning process by injecting falsified environmental data into its observation-decision-action loop.

2. **Context Poisoning**: Exploiting the knowledge components by introducing misleading information into the agent's situational awareness.

3. **Guardrail Inversion**: Weaponizing the agent's safety constraints by triggering high-priority protections that override operational objectives.

4. **Trusted Channel Exploitation**: Compromising the data pathways between distributed agent components, corrupting the information exchanged between perception and action generation components.

5. **Environment Variable Manipulation**: Modifying the runtime context parameters that inform the agent's strategy selection.

In essence, threat actors can exploit the operational environment to manipulate AI agents into executing arbitrary code or weakening defensive postures—without directly interfacing with the agent's core intelligence components or model parameters. We have taxonomized these techniques as "Indirect Agentic Flow Corruption" (AFC) attacks. The attack surface is vast and multidimensional, with AFC techniques poised to fundamentally reshape the cyber threat landscape in the coming years.

While these attacks are already occurring in production environments, they have not been systematically cataloged in security literature, as agentic AI for offensive security remains an emerging field. Our research underscores the critical necessity for human oversight in both offensive and defensive security operations, as autonomous AI systems will inevitably deviate from intended behavior patterns when subjected to sophisticated environmental manipulation without expert supervision.

## Our Test Case Evaluation

Artificial intelligence is accelerating at a rapid pace, and consequently, blue teams, red teams, and threat actors are increasingly incorporating AI into their workflows. The ability to rapidly deploy code has led many technical professionals to enhance their development methodologies for both personal and organizational advantage. One notable category includes companies developing "Fully Automated" red team and/or Penetration Testing solutions.

These companies often claim extraordinary efficiency in achieving privileged access (e.g., Domain Administrator) or discovering vulnerabilities that manual testing might overlook. Additionally, vendors promoting these automated solutions emphasize benefits such as automated reporting, continuous year-round testing capabilities, and elimination of interpersonal challenges that can arise with human consultants. Rather than aiming to replace consultants entirely, a more robust approach would involve human operators supervising these tools to prevent inadvertent exploitation. Unfortunately, the corporate vision often prioritizes workforce reduction—which has motivated our decision to release a sample of attacks that we've successfully executed.

The fundamental problem is straightforward: **dynamic decision making is not predefined**, which means there are countless ways to manipulate offensive AI tooling—and no comprehensive solution exists without constraining the AI tool's dynamic thought process (which defeats the purpose of AI-driven automation).

While the prospect of a tool that can achieve domain admin access in under 10 minutes may appeal to organizations seeking cost efficiencies, we must consider the implications when this adaptive tooling becomes a priority target for sophisticated threat actors looking to pivot within enterprise networks or deploy ransomware attacks. It's only a matter of time before APTs develop their own fully automated Agentic AI tooling. If we're transitioning to a paradigm of AI-versus-AI tools, we must acknowledge that **AI cannot fully replace human security professionals** without potentially compromising our critical infrastructure to autonomous systems that may be more susceptible to certain forms of manipulation than their human counterparts.

Again, while our test case evaluation focused specifically on exploiting autonomous offensive AI frameworks utilizing Agentic AI, the methodology can be adapted to target **any** Agentic AI framework or tool.

## Setting Expectations

The intention of this disclosure is not to impede technological progress but rather to expose significant vulnerabilities in organizational models that seek to eliminate human judgment and oversight. This paper does not represent a definitive assessment of all possible attacks, and techniques will inevitably evolve over time. Deploying fully automated security tools without proper supervision introduces significant legal and operational risks, and raising awareness of these methodologies is essential as automation expands into criminal and nation-state operations.

## Case Study Legend
Included in this repository is a folder of markdown files, with individual attack methodology & specific proof of concept steps.

Case Study 1: Compromised Windows Event Logs Lead to Security Degradation (Environmental Log Manipulation)<br>
Case Study 2: RAG Server Log Poisoning Leads to AI-Assisted Remote Code Execution & Privilege Escalation (RAG System Log Poisoning)<br>
Case Study 3: PowerShell Alias Poisoning Leads to Upstream Remote Code Execution (PowerShell Profile Manipulation)<br>
Case Study 4: Pseudo SMB "Loot" Leads to AI Assisted NTLMv2 Hash Capture (SMB Loot Baiting)<br>

## Conclusion

The case studies presented in this paper demonstrate the significant security implications of deploying autonomous AI agents for security operations without adequate human oversight. Agentic Flow Corruption attacks represent a novel and highly effective technique for compromising the integrity of AI-driven security tools by manipulating the environmental context they depend on for decision-making.

As organizations increasingly adopt AI-powered security automation, understanding these attack vectors becomes crucial for developing appropriate defensive strategies. The central challenge in addressing AFC attacks stems from the fundamental tension between an agent's autonomous decision-making capabilities and the need to constrain that autonomy to prevent manipulation.

Our research suggests that fully automated AI security tools, while offering significant operational advantages, introduce unique security vulnerabilities that traditional defense mechanisms are not designed to address. The strategic integration of human oversight within autonomous security workflows remains essential for detecting and mitigating the sophisticated environmental manipulation techniques described in this paper.

Future research should focus on developing robust validation mechanisms for environmental inputs, anomaly detection within agent decision processes, and architectural approaches that maintain agent autonomy while improving resistance to indirect manipulation.
