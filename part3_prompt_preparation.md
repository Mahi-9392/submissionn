# Part 3: Prompt Preparation

## Selected Repository
MetaGPT

## Selected Pull Request
PR #1450

---

# 3.1.1 Repository Context

MetaGPT is an open-source multi-agent AI platform in which AI agents interact similar to employees in a software company. In contrast to using one AI model for generating all artifacts, the framework involves various agents like Product Manager, Architect, Engineer, QA Engineer, and others. Each of them executes its own task and interacts with other agents in software generation process flows.

The purpose of the repository is to help developers and researchers in automatic software engineering using Large Language Models. In particular, the framework helps in automation of the generation of project plans, code, review, documentation, testing workflows.

An integral part of the repository is related to the coordination of AI agents. There is a need in proper scheduling and task synchronization to ensure interaction of AI agents occurs in an appropriate order. Proper task synchronization allows sharing of up-to-date context before execution of an agent.

The target problem area addressed in the repository is related to issues associated with the autonomous software engineering. In addition, another problem area is associated with multi-agent collaboration in software development automation.

# 3.1.2 Pull Request Description

The purpose of PR #1450 is to improve the communication process between agents inside the MetaGPT framework. In the current version, some agents may proceed further with their tasks even though they do not have the latest context provided by other agents. Such an approach leads to duplication or inconsistency in actions and output results when executing multi-agents' workflows.

The new solution addresses the problem related to messaging between agents and ensures that they are always waiting for the appropriate context until performing any actions. The solution also allows establishing a more consistent order of execution of tasks.

Moreover, the improved solution allows managing async workflow processes better since MetaGPT requires such features. Therefore, in some cases, there could be potential race conditions that lead to duplicated results if some tasks depend on others. The PR optimizes task scheduling in such a way that dependent actions will execute after the required context is generated.

Other improvements include fixing some bugs, adding additional tests, and updating some validation and workflow methods to optimize the communication between agents.

Therefore, we can conclude that the new behavior is more stable than the previous one because of proper coordination.

# 3.1.3 Acceptance Criteria

✓ If several agents perform interdependent actions, then the system should make sure that these actions will be performed in the right sequence.

✓ The implementation should guarantee that the agents will receive updated context data before proceeding with their actions.

✓ In cases when parallel asynchronous workflows are performing tasks at once, then the system should make sure that the output will not be replicated or duplicated.

✓ The implementation should correctly handle delays on the part of agents without affecting workflow performance.

✓ The communication failure between agents should be handled properly.

✓ Workflow execution pipelines should have consistent task synchronization throughout long processes.

✓ All current test cases and workflow features should function after the implementation is made.



# 3.1.4 Edge Cases

## 1. Delayed Agent Response

In some workflows, one agent may take much longer than others to complete its task. The system should ensure that dependent agents wait correctly for updated context instead of continuing execution with incomplete information. This prevents inconsistent outputs and broken workflow sequencing.


## 2. Simultaneous Async Execution

Multiple agents may execute tasks at the same time in asynchronous workflows. The implementation should prevent race conditions, duplicated message propagation, and repeated execution when several async operations access shared workflow data simultaneously.


## 3. Missing or Incomplete Shared Context

An agent may receive partial or missing context because of communication delays or execution failures. The system should validate required context before task execution and provide meaningful error handling instead of continuing with invalid state information.


## 4. Workflow Failure During Execution

If one agent crashes or fails during execution, the remaining workflow should not become corrupted. The implementation should safely stop dependent operations or trigger recovery logic without affecting other active agents.



## 5. Large Multi-Agent Workflows

When many agents participate in long-running workflows, the system should maintain stable synchronization and avoid memory or performance degradation. The implementation should handle increased communication load efficiently without causing execution bottlenecks.


# 3.1.5 Initial Prompt

You are working on the MetaGPT repository, which is a Python-based multi-agent AI framework where different AI agents collaborate to simulate software development workflows. The framework contains multiple AI roles such as Product Manager, Architect, Engineer, and QA Engineer. These agents communicate with each other using asynchronous workflows and shared execution context.

The current implementation has synchronization and coordination issues between agents during async workflow execution. In some cases, agents continue execution before receiving fully updated context from dependent agents. This can create duplicated outputs, repeated actions, incorrect execution ordering, or incomplete task processing.

Your task is to improve the internal workflow coordination and synchronization system used for communication between agents.

Requirements:

1. Update the message propagation system so agents always receive the latest shared context before starting dependent tasks.

2. Improve async task scheduling and execution ordering to reduce race conditions and duplicated execution during simultaneous operations.

3. Add validation checks to verify that required workflow context exists before execution continues.

4. Improve communication reliability between agents during long-running workflows.

5. Add proper error handling for failed communication, delayed responses, or incomplete context scenarios.

6. Ensure the implementation remains compatible with the current workflow structure and does not break existing agent APIs.

Acceptance Criteria:
- Dependent tasks should execute in the correct sequence.
- Shared context should remain synchronized between agents.
- Duplicate outputs or repeated execution should not occur during concurrent execution.
- Delayed agent responses should not break workflow execution.
- Existing workflows and unit tests should continue working after the implementation.

Edge Cases to Consider:
- Delayed async agent responses
- Missing or partially updated shared context
- Simultaneous execution of multiple dependent tasks
- Agent failure during workflow execution
- Large multi-agent workflows with heavy communication load

Testing Requirements:
- Add or update unit tests for async execution ordering.
- Verify correct message propagation between agents.
- Test concurrent execution scenarios to ensure duplicate execution does not occur.
- Validate behavior when agent communication fails or context is missing.
- Ensure no regression in existing workflows and agent interactions.

Implementation Notes:
- Follow the existing repository coding style and structure.
- Keep the implementation modular and readable.
- Avoid introducing unnecessary complexity into the workflow pipeline.
- Maintain compatibility with current async execution patterns used in the repository.

The final implementation should improve workflow stability, synchronization reliability, and execution consistency across collaborative agent workflows.