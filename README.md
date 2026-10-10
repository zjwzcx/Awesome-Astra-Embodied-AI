# Awesome Astra Embodied AI

GPT-6 Astra with embodied AI / robotics workflows and demos.

Maintained by [@zjwzcx](https://github.com/zjwzcx) ([homepage](https://xiao-chen.tech/)). Pull requests with new cases, corrections, and source updates are welcome.

## Contents

Cases are grouped by workflow and ordered by publication date, newest first within each section.

- 📊 [Public Benchmark & Evaluation Reports](#-public-benchmark--evaluation-reports)
- 🤖 [Zero-shot Control](#-zero-shot-control)
  - 🧪 [Deploy in Simulation](#-deploy-in-simulation) — 12 cases
  - 🌍 [Deploy in Real World](#-deploy-in-real-world) — 10 cases
- 🧠 [Agentic Policy Calls](#-agentic-policy-calls) — 5 cases
- 🔄 [Real-to-sim Replay / Data Rollout](#-real-to-sim-replay--data-rollout) — 8 cases
- 🛠️ [Astra Builds RL Training Environments and Training](#-astra-builds-rl-training-environments-and-training) — 6 cases

## 📊 Public Benchmark & Evaluation Reports

GPT-6 Astra is introduced in the official [OpenAI announcement](https://openai.com/index/gpt-6-astra/). Below are public evaluation repositories and result reports for GPT-6 Astra in embodied-AI settings, ordered by publication date; results are reported by the respective maintainers and should be interpreted within each project's disclosed setup.

- **[RoboCurve GPT-6 Astra evaluation](https://openai.robocurve.org/gpt-6-astra/)**: controlled YAM-arm comparison reporting 19/20 bowl-task completions and 80% fewer output tokens; published 2026-09-04.
- **[GPT-Policy-Eval](https://github.com/cheng-haha/GPT-Policy-Eval)**: one-shot transfer from a video demonstration to a real-robot, contact-rich plug-insertion task, without VLA, RL, or DAgger; published 2026-09-11.
- **[GPT-as-Policy](https://github.com/anonymous-report-421/GPT-as-Policy)**: public benchmark repository and result report evaluating GPT-6 Astra as a robot policy; published 2026-09-16.
- **[RoboDojo GPT-6 Astra evaluation](https://robodojo-benchmark.com/report/gpt-6-astra-eval)**: zero-shot evaluation via the fixed RoboProbe harness on 42 simulation tasks (2,100 trials), reporting 28.97 Average Score and 22.48% Average SR; real-robot testing was halted for safety; published 2026-09-16.
- **[RPent](https://github.com/RLinf/RPent)**: recursive-agent harness pairing an agentic planner with frozen VLA primitives, with a public [leaderboard](https://github.com/RLinf/RPent#leaderboard); GPT-6 Astra reports 92.63% on LIBERO-PRO and a chart-leading 59.20% on RoboCasa365 Target50; published 2026-09-21. See also [Case 26](#case-26-harness-vla-memory-guided-agentic-manipulation).
- **[Astra on RoboMME](https://bingaochen.github.io/Astra-on-RoboMME/)**: three-tier memory-augmented manipulation (Astra planner, fine-tuned VLA, VLM completion monitor) reporting 79.13% success (633/800) on the RoboMME test set; published 2026-09-22. See also [Case 25](#case-25-astra-on-robomme-three-tier-memory-augmented-manipulation).
- **[RoboICL](https://mosi-ai.github.io/RoboICL-GPT6-Astra.github.io/)** ([paper](https://arxiv.org/abs/2609.34261), [code](https://github.com/Mosi-AI/RoboICL)): robot control with frozen GPT-6 Astra, combining demonstration context and bounded anchored interaction memory without robot-specific parameter updates or a learned VLA; reports an overall progress score of 50.64 on 30 RoboDojo tasks (zero-shot on Open, one demonstration elsewhere), plus evaluations on three real-robot tasks; published 2026-09-28 (arXiv submission).
- **[Video2World](https://aetherlabsai.github.io/Video2World/)** ([paper](https://arxiv.org/abs/2610.04432)): benchmark of 222 tasks from 189 embodied videos where coding agents write code to rebuild interactive simulated worlds, evaluated on geometric fidelity, object-motion dynamics, and task completion; GPT-6 Astra ranks 2nd of 9 agents (V2WScore 43.55, 10.7% success) with the most accurate geometry but far below the human-assisted reference (74.2, 58.8%), showing that accurate reconstruction does not imply a functional world; published 2026-10-03.
- **[Moonlake: Evaluating a 3D Agent for Sim-Ready Assets](https://moonlakeai.com/blog/evaluating-3d-agent)** ([announcement](https://x.com/sharonal_lee/status/2107148914269032875)): sim-ready asset generation benchmark comparing Moonlake's 3D Agent against GPT-6 Astra and other baselines across 22 metrics and Isaac Sim interaction tests; reported rank score 65.2 vs Astra 47.0; published 2026-10-05.
- **[4DCodeBench](https://4dcodebench.com/)** ([paper](https://arxiv.org/abs/2610.03715), [announcement](https://x.com/zzigakovacic/status/2107153000179642438)): inverse-graphics benchmark where agents write executable code reconstructing dynamic scenes from 200 videos (100 real, 100 simulated); GPT-6 Astra [Max] leads the 18-agent ranking (Overall 0.79) and dynamics by 31%; published 2026-10-05.

## 🤖 Zero-shot Control

### 🧪 Deploy in Simulation

Astra directly performs zero-shot control in a simulator.

#### Case 1: [Dual-ALOHA Spatial-constraint Puzzles](https://x.com/qineng_wang/status/2099893504658866561)

**Source / Credit:** [Qineng Wang (@qineng_wang)](https://x.com/qineng_wang), X demo of Astra planning two Dual-ALOHA spatial-constraint tasks, with an accompanying [interactive replay and methods page](https://qinengwang-aiden.github.io/demos/constraint_demos/).

**Published:** 2026-09-15

<p align="center"><img src="assets/case-34-dual-aloha-constraint-puzzles.jpg" alt="Dual-ALOHA spatial-constraint puzzle demonstrations" width="720" /></p>

Astra plans motions that separate interlocked parts and thread a rope through three rings. The claw task is a kinematic replay from a pregrasped state; the rope task uses native MuJoCo dynamics, while both use disclosed ideal-grasp assumptions and demonstrate specific planned motions rather than an online policy.

#### Case 2: [Vision-only Humanoid Body Control](https://www.rednote.com/discovery/item/6aa7e0f6000000002b01297c?xsec_token=ABmjC06EQ2omZK2bVc-pqYOZHTFYlemRyPYY3Kj_9_a1g=&xsec_source=pc_search&source=web_search_result_notes)

**Source / Credit:** [ZQ](https://www.rednote.com/user/profile/5f20ee17000000000101c247), Rednote demo where Astra observes a simulated humanoid through the robot camera and controls its body without privileged state information.

**Published:** 2026-09-13

<p align="center"><img src="assets/case-33-vision-only-humanoid-control.jpg" alt="Vision-only humanoid control in simulation" width="720" /></p>

Astra uses camera observations to control the humanoid and adjusts its actions during execution without access to privileged simulator state.

#### Case 3: [G1 Cola Bottle Pick-up in Isaac Sim](https://x.com/RotekSong/status/2099104628562608371)

**Source / Credit:** [Flood Sung (@RotekSong)](https://x.com/RotekSong), X demo of the GPT-6 Codex agent controlling a Unitree G1 in Isaac Sim.

**Published:** 2026-09-13

<p align="center"><img src="assets/case-32-g1-cola-isaac-sim.jpg" alt="Unitree G1 picking up a cola bottle in Isaac Sim" width="720" /></p>

Astra performs high-level planning for the cola-bottle pick-up, and the GEAR-SONIC planner converts the plan into a whole-body qpos trajectory for the simulated G1 to execute.

#### Case 4: [Quadruped Task via Five-key-joint Trajectory](https://x.com/gclue_akira/status/2098300921658868185)

**Source / Credit:** [Akira Sasaki (@gclue_akira)](https://x.com/gclue_akira), X quadruped locomotion demo where Astra outputs five key-joint trajectories for MuJoCo execution.

**Published:** 2026-09-11

<p align="center"><img src="assets/case-01-quadruped-five-joint.jpg" alt="Quadruped trajectory control in MuJoCo" width="720" /></p>

Astra supplies the sparse trajectory while the low-level controller executes the quadruped behavior in MuJoCo.

#### Case 5: [G1 Navigation Trajectory Tracked by SONIC](https://x.com/RotekSong/status/2098212303263183329/video/1)

**Source / Credit:** [Flood Sung (@RotekSong)](https://x.com/RotekSong), X demo of Astra producing a navigation trajectory for SONIC to track.

**Published:** 2026-09-11

<p align="center"><img src="assets/case-01-g1-navigation.jpg" alt="Unitree G1 navigation simulation" width="720" /></p>

Astra performs high-level navigation planning, and the GEAR-SONIC planner converts the plan into a whole-body qpos trajectory for the simulated G1 to execute.

#### Case 6: [Robot Hands Solve a Rubik’s Cube](https://x.com/ZeYanjie/status/2098118164626501669)

**Source / Credit:** [Ze Yanjie (@ZeYanjie)](https://x.com/ZeYanjie), X demo titled “GPT6 Astra solved Rubik’s Cube with robot hands.”

**Published:** 2026-09-10

<p align="center"><img src="assets/case-11-rubiks-simulation.jpg" alt="Robot hands solving a Rubik's cube" width="720" /></p>

Astra performs zero-shot dexterous cube manipulation in simulation.

#### Case 7: [Dexterous Apple-stem Grasp in SuperDex](https://www.rednote.com/discovery/item/6aa27b3a000000002b025d03?xsec_token=ABWznjLAd9oNPOxPF1Mc6ZfMK0VKAVH4AMkoYwkdPqQRw=&xsec_source=pc_search&source=web_profile_page)

**Source / Credit:** [Kiki Huang](https://www.rednote.com/user/profile/62f72244000000001f0176ea), Rednote demo using the Meta SuperDex physics backend and MuJoCo rendering. The demo package is now open source in [DexLab](https://github.com/huangkiki/Dexlab/tree/main/demos/apple-stem-grasp).

**Published:** 2026-09-10

<p align="center"><img src="assets/case-14-apple-stem-sim.jpg" alt="Dexterous apple-stem grasp in simulation" width="720" /></p>

Astra controls a dexterous hand to grasp the narrow stem of an apple in simulation.

#### Case 8: [GPT-6 Astra on HumanCLAW-Bench](https://x.com/Kuvvius/status/2098038921301311753)

**Source / Credit:** [Jiawei Gu (@Kuvvius)](https://x.com/Kuvvius), X benchmark demo using the open-source HumanCLAW-Bench harness and motion generator.

**Published:** 2026-09-10

<p align="center"><img src="assets/case-02-humanclaw-bench.jpg" alt="HumanCLAW-Bench results" width="720" /></p>

Astra completes benchmark navigation and interaction tasks through the simulation harness.

#### Case 9: [Whole-body Trajectory with a Whole-body Controller](https://www.rednote.com/discovery/item/6a9fe4df00000000110341b8?xsec_token=ABMaVBcBS54ctuQIxmhMJMZVm36xy72xuPS8s6aICdfXM=&xsec_source=pc_search&source=web_profile_page)

**Source / Credit:** [橘子不是唯一的水果](https://www.rednote.com/user/profile/695bb2a2000000003702ea8f), Rednote demo where Astra generates a whole-body trajectory and a whole-body controller executes it.

**Published:** 2026-09-08

<p align="center"><img src="assets/case-24-whole-body-trajectory.jpg" alt="Whole-body trajectory simulation" width="720" /></p>

Astra generates the trajectory while the whole-body controller closes the execution loop.

#### Case 10: [Isaac Sim Cube Grasp from One Prompt](https://www.rednote.com/discovery/item/6aa017a8000000002b002341?xsec_token=ABeuYgBbxlsBRQGFSm3KRd7TFtNG2CtmpEnSxlcSsSC4E=&xsec_source=pc_like)

**Source / Credit:** [神秘小孙](https://www.rednote.com/user/profile/5b3f9fc86b58b75d4c02ccc0), Rednote demo of Astra building a depth-camera robot-arm cube-grasp scene in Isaac Sim.

**Published:** 2026-09-08

<p align="center"><img src="assets/case-20-isaac-sim.jpg" alt="Isaac Sim cube grasp" width="720" /></p>

Astra receives one task sentence and produces a working simulated grasp demo.

#### Case 11: [Physically Writing a Fibonacci Sequence](https://x.com/dimentary/status/2097455860541009958)

**Source / Credit:** [Dmytro Hrybov (@dimentary)](https://x.com/dimentary), X demo of Astra generating a Unitree G1 motion for a physical Fibonacci-writing task.

**Published:** 2026-09-08

<p align="center"><img src="assets/case-13-fibonacci-final-frames.jpg" alt="Final frames of the simulated Fibonacci-writing task" width="720" /></p>

Astra attempts a long-horizon simulated manipulation task that ends with generated code and robot motion.

#### Case 12: [LLM Harness for Tabletop Robot Control](https://x.com/DJiafei/status/2096601096705995155)

**Source / Credit:** [Jiafei Duan (@DJiafei)](https://x.com/DJiafei), X demo of a GPT-6 Astra harness solving a tabletop grasp-and-place task.

**Published:** 2026-09-06

<p align="center"><img src="assets/case-05-gpt6-llm-harness.jpg" alt="Tabletop grasp-and-place simulation" width="720" /></p>

Astra writes and runs the control loop for a simulated tabletop manipulation task.

### 🌍 Deploy in Real World

Real-robot demonstrations with explicit hardware and deployment context.

#### Case 13: [Learning to Type and Self-express on a Keyboard](https://x.com/kaiwynd/status/2098823484474348008)

**Source / Credit:** [Kaifeng Zhang (@kaiwynd)](https://x.com/kaiwynd), X demo where Astra learns to operate a keyboard with a real robot after being asked to express itself.

**Published:** 2026-09-12

<p align="center"><img src="assets/case-28-keyboard-self-expression.jpg" alt="Real robot learning to type on a keyboard" width="720" /></p>

Astra turns an open-ended semantic instruction into physical key presses, learning the robot control through visual feedback in about 40 minutes.

#### Case 14: [Marker Grasp from Low-level Control Only](https://www.rednote.com/discovery/item/6aa4d7e200000000260145ff?xsec_token=ABur_B60E14GxVQp2ei3USGtEElW40SN75Vj5aB_USVUA=&xsec_source=pc_search&source=web_profile_page)

**Source / Credit:** [star大小变](https://www.rednote.com/user/profile/69c2311e000000003203e786), Rednote demo where Astra discovers joint-to-end-effector control and grasps a marker without prior skills.

**Published:** 2026-09-12

<p align="center"><img src="assets/case-21-marker-grasp.jpg" alt="Robot arm grasping a marker" width="720" /></p>

Astra explores the robot’s joint readings and reaches a marker grasp in about 30 minutes.

#### Case 15: [GPT-Policy-Eval One-shot Plug Insertion](https://github.com/cheng-haha/GPT-Policy-Eval)

**Source / Credit:** [GPT-Policy-Eval](https://github.com/cheng-haha/GPT-Policy-Eval), one-shot video demonstration of GPT-6 Astra guiding a real robot to grasp and insert a plug with visual feedback.

**Published:** 2026-09-11

<p align="center"><img src="assets/case-27-gpt-policy-eval.jpg" alt="GPT-Policy-Eval plug insertion keyframe" width="720" /></p>

Astra executes a contact-rich plug-insertion task from a single video demonstration without VLA, RL, or DAgger; see the complementary [RoboCurve evaluation](https://openai.robocurve.org/gpt-6-astra/) for controlled robot-arm results.

#### Case 16: [Mobile Manipulation with In-context Learning](https://x.com/ax_pey/status/2098216469012283681)

**Source / Credit:** [Axel (@ax_pey)](https://x.com/ax_pey), X demo explicitly showing GPT-6 Astra in-context learning across environments, viewpoints, and layouts.

**Published:** 2026-09-11

<p align="center"><img src="assets/case-06-mobile-manipulation-icl.jpg" alt="Mobile manipulation in-context learning" width="720" /></p>

Astra infers mobile-manipulation behavior from visual context without a task-specific text prompt.

#### Case 17: [Rapid Adaptation to an Unseen Robot Embodiment](https://x.com/lucascassiano/status/2097830777438486557)

**Source / Credit:** [Lucas Cassiano (@lucascassiano)](https://x.com/lucascassiano), X demo giving Astra full access to the robot hardware and the [Vitrus AI](https://x.com/Vitrus_ai) robotics OS.

**Published:** 2026-09-09

<p align="center"><img src="assets/case-30-new-embodiment-control.jpg" alt="Astra adapting to control a previously unseen robot embodiment" width="720" /></p>

Astra learns to control a robot embodiment it has not seen before, without human egocentric data or a VLA, showing rapid online adaptation to a new control interface.

#### Case 18: [ENPIRE Robotics Harness In-context Learning](https://x.com/TongheZhang01/status/2097801107602911243)

**Source / Credit:** [Tonghe Zhang (@TongheZhang01)](https://x.com/TongheZhang01), X demo of GPT-6 Astra performing robot in-context learning through the ENPIRE harness.

**Published:** 2026-09-09

<p align="center"><img src="assets/case-07-empire-icl.jpg" alt="ENPIRE robotics harness in-context learning" width="720" /></p>

Astra learns the real-world behavior from demonstrations in context, without task-specific retraining.

#### Case 19: [Cucumber Slicing with Loop-ROS](https://www.rednote.com/discovery/item/6aa0c4900000000012034a2f?xsec_token=ABYB6HItIwwYq0Yyi9-hwoM-vMalkFRmYMAkN0iUWpTM4=&xsec_source=pc_search&source=web_profile_page)

**Source / Credit:** [盒子桥](https://www.rednote.com/user/profile/65bb8b3d000000000d03e137), Rednote demo of GPT-6 Astra directly controlling a robot through Loop-ROS.

**Published:** 2026-09-09

<p align="center"><img src="assets/case-16-cucumber-slicing.jpg" alt="Robot slicing a cucumber" width="720" /></p>

Astra controls the robot arm through the slicing sequence in the real world.

#### Case 20: [Painting the Golden Gate Bridge from a Semantic Prompt](https://x.com/cdngdev/status/2097339677128982873)

**Source / Credit:** [thijs (@cdngdev)](https://x.com/cdngdev), X demo where Astra is given a robot, a paintbrush, and a camera, then asked to paint the Golden Gate Bridge in the real world.

**Published:** 2026-09-08

<p align="center"><img src="assets/case-29-golden-gate-painting.jpg" alt="Real robot painting the Golden Gate Bridge" width="720" /></p>

Astra translates the high-level visual concept into physical brush strokes and progressively improves the painting across attempts using camera feedback.

#### Case 21: [Direct End-effector Pose Control](https://www.rednote.com/discovery/item/6a9fc0710000000029015578?xsec_token=ABMaVBcBS54ctuQIxmhMJMZSAU7Wspgd3bmCnb4tQqHsU=&xsec_source=pc_search&source=web_profile_page)

**Source / Credit:** [Loule](https://www.rednote.com/user/profile/69ddd8920000000033024ad0), Rednote demo of Astra directly outputting end-effector poses for a robot arm.

**Published:** 2026-09-08

<p align="center"><img src="assets/case-18-direct-pose.jpg" alt="Direct robot-arm pose control" width="720" /></p>

Astra places the longest piece of bread into a basket using third-person and wrist cameras.

#### Case 22: [Piper Carrot Pick-and-place](https://www.rednote.com/discovery/item/6a9bd4c80000000028037f67?xsec_token=ABLUcokp8Tzdy13Avv1khxst1pWqWBaR7JLjQhUhWsSs4=&xsec_source=pc_like)

**Source / Credit:** [虽然不但是](https://www.rednote.com/user/profile/5f5ca72900000000010061fb), Rednote demo using only Codex/GPT-6, Piper, and the RealSense SDK.

**Published:** 2026-09-05

<p align="center"><img src="assets/case-22-piper-carrot.jpg" alt="Piper robot picking a carrot" width="720" /></p>

Astra directly controls Piper through repeated visual pick-and-place attempts.

## 🧠 Agentic Policy Calls

Astra performs high-level task understanding and decomposition, then calls a pretrained embodied foundation model for low-level control.

#### Case 23: [SimEX: Simulation-Integrated Robotics AutoResearch](https://robo-simex.github.io/)

**Source / Credit:** Jiaheng Hu, Roberto Martín-Martín, Peter Stone, Rocky Duan, Zhenyu Jiang, and Guanya Shi (UT Austin, Amazon FAR, CMU) — [Project Page](https://robo-simex.github.io/), [Paper](https://arxiv.org/abs/2609.38982).

**Published:** 2026-09-30 (arXiv submission)

A coding agent autoresearches robot skills in simulation instead of on hardware: open-ended probe-and-optimize cycles turn self-discovered failures into sub-goals and grow a toolbox of perception/action primitives, then five real-robot trials adapt the toolbox and the simulator together — each trial is replayed in simulation to diagnose the failure and screen candidate repairs before the next trial. At deployment the agent writes a fresh code-as-policies script per instruction against the toolbox, with no demonstrations and no learned policy. On a real dual-arm YAM robot it performs barcode scanning, plate-to-tote, and towel folding with about ten minutes of robot time per task; controlled sim-to-sim evaluations reach 83% / 97% / 54% success after adaptation, versus 0% / 37% / 29% for a no-simulation ablation.

#### Case 24: [Distilling Astra’s Capabilities into a Playbook](https://seungyeon.me/RHD/)

**Source / Credit:** [Seungyeon Kim et al.](https://arxiv.org/abs/2609.33378), Recursive Harness Distillation (RHD). [Project Page](https://seungyeon.me/RHD/), [Paper](https://arxiv.org/abs/2609.33378), [Hugging Face](https://huggingface.co/papers/2609.33378), and [LinkedIn](https://www.linkedin.com/posts/seungyeonkim1_embodiedai-robotics-vla-activity-7510680971252535296-W-3S).

**Published:** 2026-09-27 (arXiv submission)

https://github.com/user-attachments/assets/7ee7102c-1efe-482e-8ec8-2cb581495e99

Astra distills its robotic problem-solving experience into a playbook and recursively refines it through Luna’s execution feedback, enabling the cheaper Luna agent to guide a frozen VLA.

#### Case 25: [Astra on RoboMME: Three-tier memory-augmented manipulation](https://bingaochen.github.io/Astra-on-RoboMME/)

**Source / Credit:** Bingao Chen, Haoquan Fang, and C. Karen Liu (Stanford University) — [Blog](https://bingaochen.github.io/Astra-on-RoboMME/), [Videos](https://bingaochen.github.io/Astra-on-RoboMME/#videos), and [Code](https://github.com/bingaochen/Astra-on-RoboMME).

**Published:** 2026-09-22 (project website)

GPT-6 Astra plans grounded subtasks from task instructions and visual history, a fine-tuned π0.5 VLA executes them, and a fine-tuned Qwen3-VL-4B model monitors subtask completion. Completion events trigger new Astra planning calls, while the VLA continues executing the current subtask between calls. This three-tier system separates frequent progress checks from high-level reasoning for memory-dependent manipulation in simulation; see the [evaluation report](#-public-benchmark--evaluation-reports) for results on RoboMME.

#### Case 26: [Harness VLA: Memory-guided agentic manipulation](https://harnessvla.github.io/)

**Source / Credit:** Harness VLA / RPent team — [Project](https://harnessvla.github.io/), [Video](https://harnessvla.github.io/#video-introduction), [Paper](https://arxiv.org/abs/2607.08448), and [Code (RPent)](https://github.com/RLinf/RPent).

**Published:** 2026-09-17 (video added to the project page)

<p align="center"><img src="assets/harnessvla-rpent-recovery-sequence.jpg" alt="Nine chronological frames of Harness VLA sorting dirty and clean plates, detecting a failed grasp, retrying, and placing the plates in their respective containers" width="720" /></p>

GPT-6 Astra acts as the planner in RPent, combining memory and visual feedback to compose frozen VLA calls with a fixed library of analytic motion primitives. The real-robot demonstration shows task retargeting, ordered execution, sorting, and recovery from failed grasps without fine-tuning the VLA. The sequence above follows one plate-sorting task from a failed grasp through retry and placement.

#### Case 27: [Zero-shot Task Execution through FluxVLA](https://www.rednote.com/discovery/item/6aa16835000000000b00f46d?xsec_token=ABDcu5eBZZYkAUcveAv8IZNWsbLmXk6CUM5u5BhDPODB0=&xsec_source=pc_search&source=web_profile_page)

**Source / Credit:** [Jikun](https://www.rednote.com/user/profile/5e25bcdc00000000010085a8), Rednote demo pairing GPT-6 Astra with the pretrained [FluxVLA](https://github.com/FluxVLA/FluxVLA) policy.

**Published:** 2026-09-09

<p align="center"><img src="assets/case-19-fluxvla.jpg" alt="FluxVLA closed-loop robot execution" width="720" /></p>

“Zero-shot” refers to Astra’s task inference and planning; FluxVLA executes the low-level embodied actions.

## 🔄 Real-to-sim Replay / Data Rollout

Workflows that reconstruct or replay real-world trajectories, demonstrations, and environments in simulation.

#### Case 28: [Mocap Whip-Cracking and Lasso Retargeting on Real Arms](https://krishnasuresh.org/blog/2026/robot-whips/)

**Source / Credit:** [Krishna Suresh](https://krishnasuresh.org/blog/2026/robot-whips/), blog post from the Robotics and AI Institute demonstrating Vicon-mocap human demonstrations retargeted to an OpenarmX and an xArm7 for whip cracking and cleat lassoing.

**Published:** 2026-09-26

<p align="center"><img src="assets/case-37-robot-whips.png" alt="Robot trajectory tracking a human whip-crack demonstration" width="720" /></p>

Astra automatically implements the demonstration-replay pipeline from a single prompt by composing open-source tools (drake, casadi, pinocchio, pink, mjlab): inverse kinematics warm-starts a dynamics-constrained trajectory optimization that tracks the mocap hand motion, and Astra additionally generates the calibration-data collection script, the dynamics model, and an inverse dynamics controller. The robots then execute the trajectories open-loop and reproduce dynamic manipulation skills such as cracking a whip, without any policy learning; imperfect tracking still succeeds when the whip's own physics completes the motion.

#### Case 29: [Real2Sim2Real RL: Humanoid Cart-pushing in a Reconstructed Office](https://www.rednote.com/discovery/item/6ab34cfd0000000018005cab?xsec_token=CBoKOnuhKTqoyv12enaYThxB4L_a-12BnOafHa5vF3aRw=&xsec_source=app_share)

**Source / Credit:** [watchtower](https://www.rednote.com/user/profile/5e38ca4e00000000010034fa), Rednote demo of a full GPT-6 Astra real-to-sim-to-real loop on a humanoid robot in an office.

**Published:** 2026-09-23

<p align="center"><img src="assets/case-36-office-real2sim2real.jpg" alt="Real humanoid robot pushing a cart through an office doorway after real2sim2real RL training" width="720" /></p>

Astra rebuilds the real office as a simulation scene (real2sim), estimates contact points and other key supervision signals, and trains a reinforcement-learning manipulation policy from them. In the reconstructed scene it decides where to grasp and where to push while SONIC drives the humanoid's whole-body motion, and the trained policy is then deployed back onto the real robot (sim2real), which pushes a cart through the doorway. The posted video runs at real speed in a single unedited take, and longer-horizon tasks are planned.

#### Case 30: [Lab Kitchen Reconstruction with Articulated Objects](https://www.rednote.com/discovery/item/6aa4d64c000000000b037809?xsec_token=ABur_B60E14GxVQp2ei3USGkgJntlivJm_02tlDaUFWmg=&xsec_source=pc_search&source=web_profile_page)

**Source / Credit:** [Frank ZY Dou](https://www.rednote.com/user/profile/5e3431cf0000000001002919), Rednote demo reconstructing a lab kitchen from a 20-second monocular RGB video with movable cabinets and other articulated structures.

**Published:** 2026-09-12

<p align="center"><img src="assets/case-15-articulated-kitchen.jpg" alt="Reconstructed lab kitchen with articulated objects" width="720" /></p>

Astra iteratively models a real kitchen and its articulated objects into a simulation scene.

#### Case 31: [Rope-driven Dexterous Hand Reconstruction](https://x.com/dimentary/status/2097857980150763900)

**Source / Credit:** [Dmytro Hrybov (@dimentary)](https://x.com/dimentary), X attempt to recreate 1X's tendon-driven hand demo from a reference video in MuJoCo.

**Published:** 2026-09-10

<p align="center"><img src="assets/case-12-rope-hand-failure.jpg" alt="Partial rope-driven hand reconstruction in MuJoCo" width="720" /></p>

Astra rebuilds the hand and motion, but uses simplified mechanics and illustrative cable deformation rather than full tendon-transmission physics.

#### Case 32: [Tendon-driven Dexterous Hand Motion Reconstruction](https://x.com/earthtojake/status/2097789988670709821)

**Source / Credit:** [Jake Fitzgerald (@earthtojake)](https://x.com/earthtojake), X demo in which Astra designs and reconstructs the motion of a tendon-driven robot hand.

**Published:** 2026-09-09

<p align="center"><img src="assets/case-31-tendon-hand-design.jpg" alt="Tendon-driven dexterous hand designed by Astra" width="720" /></p>

Astra reconstructs the tendon-driven hand's motion in a simulated model, including cable-actuated finger movement.

#### Case 33: [Dexterous Hand-object Data Rollout](https://x.com/Lingxiao234/status/2097717020540481630)

**Source / Credit:** [Lingxiao (@Lingxiao234)](https://x.com/Lingxiao234), X demo showing two videos driving real-to-sim reconstruction and physical retargeting to Wuji hands.

**Published:** 2026-09-09

<p align="center"><img src="assets/case-10-hand-object-rollout.jpg" alt="Dexterous hand-object real-to-sim rollout" width="720" /></p>

Astra reconstructs hand-object interaction from videos without explicit states or actions.

#### Case 34: [Video in → Physics out](https://x.com/huxiao93612565/status/2097815230105399402)

**Source / Credit:** [xiao hu (@huxiao93612565)](https://x.com/huxiao93612565), X demo of Astra writing hand tracking, IK retargeting, and grasp-refinement code for a 44-DOF hand.

**Published:** 2026-09-09

<p align="center"><img src="assets/case-03-video-to-physics.jpg" alt="Video-to-physics dexterous hand retargeting" width="720" /></p>

Astra turns visual hand motion into a physics-backed dexterous-hand replay.

#### Case 35: [Multi-view Real-to-sim Reconstruction](https://x.com/Lingxiao234/status/2096992059731443923)

**Source / Credit:** [Lingxiao (@Lingxiao234)](https://x.com/Lingxiao234), X demo combining multi-view RGB, robot actions, camera calibration, assets, system identification, MuJoCo, and Blender.

**Published:** 2026-09-07

<p align="center"><img src="assets/case-09-multiview-realsim.jpg" alt="Multi-view real-to-sim reconstruction" width="720" /></p>

Astra builds a replayable simulator from demonstrations, geometry, and physical parameters.

## 🛠️ Astra Builds RL Training Environments and Training

Workflows where Astra helps create environments, task definitions, training code, and experiment iterations.

#### Case 36: [Sharpa Hand Pen-spinning RL in Isaac Lab](https://x.com/walterzhu8/status/2100212420840989112)

**Source / Credit:** [Wentao Zhu (@walterzhu8)](https://x.com/walterzhu8), X report of an autonomous Astra run by his student Chengyang Li to build and train a dexterous-hand pen-spinning task.

**Published:** 2026-09-16

<p align="center"><img src="assets/case-35-sharpa-pen-spinning-rl.jpg" alt="Sharpa Wave dexterous hand spinning a pen with a PPO policy in Isaac Lab" width="720" /></p>

Astra creates the pen mesh, implements the Sharpa-hand task in Isaac Lab, trains the PPO policy, and produces a visualization video during an autonomous run of about a day and a half.

#### Case 37: [RL-trained Duck Robot Demo](https://www.rednote.com/discovery/item/6aa347e2000000000b036667?xsec_token=AB1z4k50CvQ0PFZpqtQXWYlVMONqE2yr3ER8jk-hVWI74=&xsec_source=pc_search&source=web_profile_page)

**Source / Credit:** [拂晓时分_茉莉飘香](https://www.rednote.com/user/profile/5ffbc96d00000000010060ae), Rednote demo reporting an RL-trained duck robot generated from one image and one description.

**Published:** 2026-09-11

<p align="center"><img src="assets/case-26-duck-rl.jpg" alt="RL-trained duck robot in simulation" width="720" /></p>

Astra builds and trains a locomotion demo from a compact visual specification.

#### Case 38: [Quadruped Locomotion System from RL](https://x.com/gclue_akira/status/2098300921658868185)

**Source / Credit:** [Akira Sasaki (@gclue_akira)](https://x.com/gclue_akira), X report of Astra designing a robot dog, iterating 25 loops in five days, and training nine motions with RL.

**Published:** 2026-09-11

<p align="center"><img src="assets/case-08-quadruped-rl.jpg" alt="Quadruped locomotion reinforcement-learning result" width="720" /></p>

Astra co-designs the quadruped and trains a simulated locomotion system; real-hardware debugging is planned rather than completed.

#### Case 39: [Dexterous In-hand Manipulation RL](https://www.rednote.com/discovery/item/6aa3e146000000002b0123dc?xsec_token=AB5n_GSvnshtGoIJqykTNpkWlIS-zHnIYe2n5pAiGLSgw=&xsec_source=pc_like)

**Source / Credit:** [十一](https://www.rednote.com/user/profile/610bc8f100000000200284e2), Rednote RL demo of a dexterous hand manipulating a walnut; self-collision was not enabled in the reported run.

**Published:** 2026-09-11

<p align="center"><img src="assets/case-17-inhand-rl.jpg" alt="Dexterous in-hand manipulation RL" width="720" /></p>

Astra trains the in-hand manipulation behavior while exposing the reported collision-model limitation.

#### Case 40: [Office Scan → Newton / G1 Humanoid Gym](https://x.com/Jiarui_X/status/2098439950991806804)

**Source / Credit:** [Jiarui Xu (@Jiarui_X)](https://x.com/Jiarui_X), X demo where Astra rebuilds an office scan in Blender, exports USD, and creates a G1 walking scene in Newton.

**Published:** 2026-09-11

<p align="center"><img src="assets/case-04-office-scan-newton.jpg" alt="Office scan rebuilt in Newton for a G1 robot" width="720" /></p>

Astra creates the environment and training-ready humanoid simulation scene.

#### Case 41: [Isaac Sim Environment, PPO Training, and Tuning](https://www.rednote.com/discovery/item/6aa29087000000002600bb2e?xsec_token=ABupW63bXfa1dAqIk6vaYviNev-xOXuTmePvxk8Su9NK4=&xsec_source=pc_collect)

**Source / Credit:** [十一](https://www.rednote.com/user/profile/610bc8f100000000200284e2), Rednote demo of Astra building an Isaac Sim RL environment, configuring PPO, and tuning the run.

**Published:** 2026-09-10

<p align="center"><img src="assets/case-23-rl-training.jpg" alt="Isaac Sim reinforcement-learning training" width="720" /></p>

Astra handles environment construction, training configuration, and iteration in one workflow.

## ⚠️ Failure Cases

These entries index representative partial or unsuccessful outcomes. A failure can reflect modeling, calibration, embodiment, or tool limits in one setup and does not prove that Astra lacks the underlying capability.

- [Rope-driven Dexterous Hand Reconstruction](#case-31-rope-driven-dexterous-hand-reconstruction): partial real-to-sim reconstruction with simplified tendon mechanics and illustrative cable deformation; full tendon-transmission physics remains unfinished.

## 🙏 Credits

Credit belongs to the original authors, projects, and posts referenced by each case. This repository is a non-commercial compilation and technical analysis only; it does not claim ownership of the underlying work. Pull requests with new cases, corrections, and source updates are welcome.
