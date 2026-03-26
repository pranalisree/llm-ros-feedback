# llm-ros-feedback
A closed-loop robotic planning system that uses LLM-generated expected states and execution feedback to detect failures and replan dynamically, improving task success in ManiSkill environments.

## Overview

This project explores how to improve robotic task execution by integrating **state verification and feedback-driven replanning** into an LLM-based planning pipeline.

Traditional LLM-based robotic planners generate a sequence of actions and execute them in a one-shot manner. However, these systems often fail when real-world execution diverges from the planned trajectory, as they lack mechanisms to detect and recover from failure.

To address this, we implement a **closed-loop planning architecture** where:

* A large language model (LLM) generates a high-level task plan
* A planner converts the plan into executable PDDL steps
* The LLM then predicts the **expected environment state after each step**
* During execution, the robot returns the **actual state** after each step
* The system compares expected vs. actual states:

  * If they match → execution continues
  * If they diverge → the remaining plan is discarded and the system **replans from the current state**

This enables the system to dynamically adapt to failures rather than blindly executing an invalid plan.

---

## Key Idea

> Use the LLM not only for planning, but also for **predicting expected states**, and leverage state mismatches as a signal for **failure detection and replanning**.

---

## Experimental Focus

We evaluate this approach in ManiSkill home-domain environments by comparing:

* A **baseline one-shot planning pipeline** (no feedback)
* A **feedback-based system** with stepwise state verification and replanning

We measure:

* Task completion rate
* Plan Execution Alignment (PEA)
* Recovery rate after failure

---

## Why This Matters

Robotic systems operating in real-world environments must handle uncertainty, execution errors, and dynamic changes. By incorporating feedback into the planning loop, this project aims to improve:

* robustness to failure
* adaptability during execution
* alignment between symbolic plans and physical outcomes

---

## Tech Stack

* LLM-based planning
* PDDL (symbolic planning)
* ManiSkill simulation environment
* Python-based execution and evaluation

---

## Repo Structure

```bash
/baseline        # One-shot planning pipeline
/feedback        # Feedback + replanning system
/environment     # ManiSkill setup and configs
/metrics         # Evaluation + logging
/data            # Experiment results
/docs            # Design + reports
```

