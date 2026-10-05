**Volume 21. Quadruped Robot Software**


# Chapter 09. Quadruped Manipulation

##  

## 09.01. Quadruped with Arm Loco Manipulation Overview

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

A quadruped equipped with a manipulator extends legged mobility into loco-manipulation, where locomotion and object interaction are treated as parts of one coordinated physical task. Instead of moving to a fixed pose and operating the arm independently, the robot can reposition its body, adjust footholds, regulate balance, and move the end effector together. This capability is central to the chapter structure, which progresses from arm-base coordination to mobile grasping, valve operation, payload handling, dynamic manipulation, tool use, and industrial applications. Volume_21_Quadruped_Robot_Softw...

The main advantage of an arm-equipped quadruped is the combination of terrain accessibility and manipulation reach. A wheeled mobile manipulator is constrained by traversable floor geometry, while a fixed manipulator is constrained by its installation location. A quadruped can walk across stairs, debris, slopes, gaps, and irregular surfaces, then use body translation, body orientation, leg configuration, and arm motion to establish an effective manipulation pose. The locomotion system therefore becomes an active component of the manipulator workspace rather than merely a transportation mechanism.

This integration also creates a tightly coupled dynamics problem. Motion of the arm changes the robot\'s center of mass, centroidal momentum, joint loading, and ground reaction force distribution. Manipulating a heavy object or applying force to a valve can introduce external forces and moments that disturb the stance. Conversely, body motion changes the arm\'s reference frame and end-effector trajectory. Successful loco-manipulation must therefore account for leg contacts, base dynamics, arm dynamics, payload effects, actuator limits, friction constraints, and task objectives within a coordinated control architecture.

A useful software decomposition separates perception, task planning, locomotion planning, manipulation planning, state estimation, whole-body coordination, and low-level control while preserving continuous information exchange among them. Perception estimates terrain geometry, object pose, grasp regions, contact conditions, and free space. The task layer determines what interaction should occur, while locomotion and manipulation planners generate compatible body, foothold, and end-effector objectives. Whole-body control then converts these objectives into dynamically feasible forces, accelerations, or joint commands.

Whole-body control is especially important because the quadruped may possess more controllable degrees of freedom than are required by a single manipulation objective. Task hierarchies can prioritize balance, contact maintenance, collision avoidance, end-effector tracking, posture regulation, and joint-limit avoidance. Optimization-based controllers can distribute motion across the legs, floating base, and manipulator so that the arm does not need to accomplish the entire Cartesian displacement alone. This directly connects quadruped manipulation with the preceding whole-body-control framework, including explicit manipulation-arm integration. Volume_21_Quadruped_Robot_Softw...

Manipulation can be performed in several mobility regimes. In a stationary regime, the robot establishes a stable stance before moving the arm, simplifying control and providing a relatively predictable manipulation frame. In a repositioning regime, the quadruped alternates walking and manipulation to enlarge its effective workspace. Fully dynamic loco-manipulation is more demanding because locomotion and arm motion occur simultaneously. The controller must then maintain end-effector accuracy despite periodic body motion, changing contacts, impacts, and terrain-induced disturbances.

Arm-base coordination provides a major workspace benefit. When an object lies outside the instantaneous arm workspace, the robot can translate or rotate its trunk instead of declaring the target unreachable. Body height can be changed to access low or elevated objects, and body roll or pitch can improve arm geometry on sloped terrain. Foot placements can also be selected to create a stance favorable for forceful manipulation. Reachability consequently becomes a whole-body property determined jointly by terrain, contacts, body configuration, manipulator kinematics, and environmental constraints.

Perception for loco-manipulation must support both mobility and interaction. Cameras and LiDAR can provide environmental geometry and obstacle information, while wrist cameras, depth sensors, and force-torque sensing can improve local manipulation accuracy. Proprioceptive measurements provide joint state and contact information needed for balance and disturbance estimation. Because the robot itself moves substantially during operation, transformations among world, body, arm-base, sensor, object, and end-effector frames must remain temporally consistent throughout the task.

Contact-rich operations introduce additional requirements beyond free-space trajectory tracking. Opening a door, rotating a valve, pushing a lever, or operating a tool creates constraints between the end effector and environment. The desired interaction may require controlled force along one direction while allowing motion along another. Impedance, admittance, force, or hybrid motion-force control can be combined with whole-body stabilization so that interaction forces do not destabilize the supporting legs. Contact transitions must also be detected reliably because unexpected sticking or slipping can rapidly alter system dynamics.

Mobile grasping illustrates the coupling particularly clearly. The robot must detect an object, select a feasible grasp, determine whether the target can be reached from the current configuration, and reposition when necessary. During approach, locomotion perception must continue to protect foothold safety while manipulation perception refines object pose. After grasp closure, the object becomes part of the effective mechanical system, altering mass distribution and collision geometry. Subsequent walking therefore requires payload-aware balance, motion planning, and manipulation control rather than simply holding the arm at a fixed joint configuration.

Payload transport further demonstrates why locomotion and manipulation cannot be engineered independently. An arm holding a payload can shift the combined center of mass away from the nominal support region and increase joint torque requirements. Acceleration of the payload generates inertial disturbances, particularly during gait transitions or rapid body motion. A practical controller can compensate by modifying base posture, gait speed, foothold locations, arm configuration, and ground reaction forces. Payload estimation and actuator thermal limits become important when operations continue for extended periods.

Planning must also consider environmental interaction at several spatial scales. A global planner may bring the quadruped near a workstation, while a local planner chooses an approach region compatible with terrain and manipulation requirements. A whole-body planner can then search for feasible base poses, stance configurations, arm trajectories, and contacts. Rather than optimizing navigation distance alone, the system should consider manipulation reachability, visibility, stability margin, collision clearance, force capability, and escape or recovery options when selecting the final working configuration.

Learning-based methods provide another path for solving highly coupled loco-manipulation problems. Reinforcement learning can optimize coordinated leg, body, and arm behaviors that are difficult to describe using manually constructed rules, while imitation learning can transfer demonstrations of complex interaction sequences. Policies may receive proprioceptive state, terrain observations, object information, task commands, and previous actions. However, learned control must still respect physical constraints, actuator limits, collision boundaries, and safety requirements, particularly when deployed around industrial equipment or people.

Robustness is essential because real manipulation targets rarely match ideal models. Object pose estimates contain uncertainty, terrain can deform or slip, grasp contacts can shift, and interaction forces may differ from simulation. A production system therefore needs feedback throughout the complete action rather than relying on an open-loop sequence. Failed grasps, unreachable targets, excessive contact forces, loss of foothold confidence, or balance degradation should trigger recovery behaviors such as arm retraction, stance widening, body repositioning, re-perception, or safe task termination.

Safety must be enforced across both locomotion and manipulation layers. Joint position, velocity, torque, contact force, and end-effector speed limits should be complemented by stability and collision constraints. A manipulation command that is individually safe for the arm may still be unsafe for the complete robot if it produces excessive base moment or reduces foothold stability. Likewise, an otherwise valid gait may become unsafe while carrying an extended payload. Supervisory logic should therefore evaluate the coupled robot state and provide controlled degradation, protective stopping, or posture recovery.

The resulting arm-equipped quadruped should be understood as a mobile physical interaction system rather than a walking robot with an accessory manipulator. Its useful capability emerges from coordinated perception, terrain-aware locomotion, manipulation planning, whole-body control, contact reasoning, learning, and safety supervision. This perspective provides the foundation for subsequent treatment of arm-base coordination, inspection control, mobile grasping, door and valve interaction, payload placement, learned loco-manipulation, dynamic manipulation, tool use, and industrial deployment.

매니퓰레이터(Manipulator)를 장착한 4족 보행 로봇(Quadruped)은 다리 기반 이동성(Legged Mobility)을 로코-매니퓰레이션(Loco-Manipulation)으로 확장하며, 여기에서는 이동(Locomotion)과 객체 상호작용(Object Interaction)을 하나의 통합된 물리 작업(Physical Task)으로 취급한다. 고정된 자세로 이동한 후 로봇 팔을 독립적으로 작동시키는 대신, 로봇은 몸체 위치를 재조정하고 발 디딤 위치(Foothold)를 변경하며 균형을 제어하는 동시에 말단장치(End Effector)를 움직일 수 있다. 이러한 능력은 팔-베이스 협조(Arm-Base Coordination), 이동 중 파지(Mobile Grasping), 밸브 조작, 페이로드(Payload) 처리, 동적 조작(Dynamic Manipulation), 도구 사용(Tool Use), 산업 응용(Industrial Application)으로 이어지는 4족 보행 로봇 조작의 핵심 기반이다.

로봇 팔이 장착된 4족 보행 로봇의 가장 큰 장점은 지형 접근성(Terrain Accessibility)과 조작 도달 범위(Manipulation Reach)를 결합할 수 있다는 것이다. 바퀴형 이동 매니퓰레이터(Wheeled Mobile Manipulator)는 주행 가능한 바닥 형상에 의해 제약되고, 고정형 매니퓰레이터(Fixed Manipulator)는 설치 위치에 의해 작업 영역이 제한된다. 반면 4족 보행 로봇은 계단, 잔해, 경사면, 틈, 불규칙 지형을 이동한 후 몸체의 병진과 회전, 다리 자세, 로봇 팔의 움직임을 함께 이용하여 효과적인 조작 자세(Manipulation Pose)를 형성할 수 있다. 따라서 이동 시스템은 단순한 운송 수단이 아니라 매니퓰레이터 작업공간(Manipulator Workspace)을 확장하는 능동적인 구성 요소가 된다.

이러한 통합은 강하게 결합된 동역학 문제(Coupled Dynamics Problem)를 발생시킨다. 로봇 팔의 움직임은 로봇의 질량중심(Center of Mass), 중심 운동량(Centroidal Momentum), 관절 부하(Joint Loading), 지면 반력 분포(Ground Reaction Force Distribution)를 변화시킨다. 무거운 물체를 조작하거나 밸브에 힘을 가하면 외력과 외부 모멘트가 발생하여 지지 자세를 교란할 수 있다. 반대로 몸체의 움직임은 로봇 팔의 기준 좌표계와 말단장치 궤적을 변화시킨다. 따라서 성공적인 로코-매니퓰레이션은 다리 접촉, 베이스 동역학, 로봇 팔 동역학, 페이로드 영향, 액추에이터 한계, 마찰 제약조건(Friction Constraint), 작업 목표를 하나의 협조 제어 구조에서 고려해야 한다.

효과적인 소프트웨어 구조(Software Architecture)는 인지(Perception), 작업 계획(Task Planning), 이동 계획(Locomotion Planning), 조작 계획(Manipulation Planning), 상태 추정(State Estimation), 전신 협조(Whole-Body Coordination), 저수준 제어(Low-Level Control)를 분리하면서도 이들 사이에서 지속적으로 정보를 교환하도록 구성할 수 있다. 인지 시스템은 지형 형상, 객체 자세(Object Pose), 파지 영역(Grasp Region), 접촉 상태, 자유 공간(Free Space)을 추정한다. 작업 계층은 수행해야 할 상호작용을 결정하고, 이동 및 조작 계획기는 서로 호환되는 몸체, 발 디딤 위치, 말단장치 목표를 생성한다. 이후 전신 제어(Whole-Body Control)는 이러한 목표를 동역학적으로 실행 가능한 힘, 가속도 또는 관절 명령으로 변환한다.

전신 제어(Whole-Body Control)는 4족 보행 로봇이 하나의 조작 목표에 필요한 것보다 많은 제어 자유도(Degree of Freedom)를 가질 수 있기 때문에 특히 중요하다. 작업 계층(Task Hierarchy)은 균형 유지, 접촉 유지, 충돌 회피, 말단장치 추종, 자세 조절, 관절 한계 회피 등에 우선순위를 부여할 수 있다. 최적화 기반 제어기(Optimization-Based Controller)는 다리, 부유 베이스(Floating Base), 매니퓰레이터 사이에 움직임을 분배하여 전체 카테시안 변위(Cartesian Displacement)를 로봇 팔만으로 수행할 필요가 없도록 한다. 이러한 구조를 통해 4족 보행 로봇 조작은 매니퓰레이션 암 통합(Manipulation Arm Integration)을 포함한 전신 제어 프레임워크와 직접 연결된다.

조작은 여러 이동 상태(Mobility Regime)에서 수행될 수 있다. 정지 상태(Stationary Regime)에서는 로봇이 안정적인 지지 자세를 만든 후 로봇 팔을 움직이므로 제어가 단순해지고 비교적 예측 가능한 조작 기준 좌표계를 확보할 수 있다. 재배치 상태(Repositioning Regime)에서는 4족 보행과 조작을 번갈아 수행하여 유효 작업공간을 확장한다. 완전한 동적 로코-매니퓰레이션(Dynamic Loco-Manipulation)은 이동과 로봇 팔 움직임이 동시에 발생하기 때문에 더욱 어렵다. 이 경우 제어기는 주기적인 몸체 운동, 변화하는 접촉 상태, 충격, 지형에 의한 외란에도 말단장치 정확도를 유지해야 한다.

팔-베이스 협조(Arm-Base Coordination)는 작업공간을 크게 확장한다. 객체가 현재 로봇 팔 작업공간 밖에 있는 경우, 로봇은 목표를 도달 불가능한 것으로 판단하는 대신 몸통을 병진 또는 회전시킬 수 있다. 낮거나 높은 객체에 접근하기 위해 몸체 높이를 변경할 수 있으며, 경사 지형에서는 몸체의 롤(Roll)이나 피치(Pitch)를 조절하여 로봇 팔의 기구학적 조건을 개선할 수 있다. 또한 큰 힘이 필요한 조작 작업에 유리하도록 발 디딤 위치를 선택할 수도 있다. 따라서 도달 가능성(Reachability)은 지형, 접촉 상태, 몸체 자세, 매니퓰레이터 기구학, 환경 제약조건이 함께 결정하는 전신 특성(Whole-Body Property)이 된다.

로코-매니퓰레이션을 위한 인지(Perception)는 이동과 상호작용을 모두 지원해야 한다. 카메라와 라이다(LiDAR)는 환경 형상과 장애물 정보를 제공할 수 있으며, 손목 카메라(Wrist Camera), 깊이 센서(Depth Sensor), 힘-토크 센서(Force-Torque Sensor)는 국부적인 조작 정확도를 향상시킬 수 있다. 고유수용성 측정(Proprioceptive Measurement)은 균형 및 외란 추정에 필요한 관절 상태와 접촉 정보를 제공한다. 로봇 자체가 작업 중 크게 움직이기 때문에 월드(World), 몸체(Body), 팔 베이스(Arm Base), 센서(Sensor), 객체(Object), 말단장치 좌표계 사이의 변환은 전체 작업 과정에서 시간적으로 일관되게 유지되어야 한다.

접촉 중심 작업(Contact-Rich Operation)은 자유공간 궤적 추종(Free-Space Trajectory Tracking)을 넘어서는 추가 요구사항을 가진다. 문을 열거나 밸브를 돌리고, 레버를 밀거나 도구를 조작하는 과정에서는 말단장치와 환경 사이에 제약조건이 형성된다. 원하는 상호작용은 특정 방향으로 힘을 제어하면서 다른 방향의 움직임을 허용해야 할 수도 있다. 임피던스 제어(Impedance Control), 어드미턴스 제어(Admittance Control), 힘 제어(Force Control), 하이브리드 운동-힘 제어(Hybrid Motion-Force Control)를 전신 안정화와 결합하면 상호작용력이 지지 다리를 불안정하게 만드는 것을 방지할 수 있다. 예상하지 못한 고착이나 미끄러짐은 시스템 동역학을 급격히 변화시킬 수 있으므로 접촉 전환(Contact Transition) 역시 신뢰성 있게 감지해야 한다.

이동형 파지(Mobile Grasping)는 이러한 결합 관계를 명확하게 보여준다. 로봇은 객체를 감지하고 적절한 파지를 선택하며, 현재 자세에서 목표에 도달할 수 있는지를 판단한 후 필요하면 몸체 위치를 재조정해야 한다. 접근 과정에서도 이동 인지 시스템은 안전한 발 디딤을 지속적으로 보장해야 하며, 조작 인지 시스템은 객체 자세를 더욱 정밀하게 추정해야 한다. 파지가 완료되면 객체는 실질적으로 로봇 기계 시스템의 일부가 되어 질량 분포와 충돌 형상을 변화시킨다. 따라서 이후의 보행에서는 로봇 팔의 관절 자세를 단순히 고정하는 것이 아니라 페이로드를 고려한 균형, 운동 계획, 조작 제어가 필요하다.

페이로드 운반(Payload Transport)은 이동과 조작을 독립적으로 설계할 수 없는 이유를 더욱 분명하게 보여준다. 로봇 팔이 페이로드를 들고 있으면 전체 시스템의 결합 질량중심이 정상적인 지지 영역에서 벗어날 수 있으며 관절 토크 요구량도 증가한다. 특히 보행 전환이나 빠른 몸체 운동 중에는 페이로드 가속으로 관성 외란(Inertial Disturbance)이 발생한다. 실용적인 제어기는 몸체 자세, 보행 속도, 발 디딤 위치, 로봇 팔 자세, 지면 반력을 조정하여 이를 보상할 수 있다. 장시간 작업에서는 페이로드 추정(Payload Estimation)과 액추에이터 열 한계(Actuator Thermal Limit)도 중요한 요소가 된다.

계획 시스템(Planning System)은 여러 공간적 규모에서 환경과의 상호작용을 고려해야 한다. 전역 계획기(Global Planner)는 4족 보행 로봇을 작업 위치 근처까지 이동시키고, 지역 계획기(Local Planner)는 지형과 조작 요구조건을 만족하는 접근 영역을 선택할 수 있다. 이후 전신 계획기(Whole-Body Planner)는 실행 가능한 베이스 자세, 지지 자세, 로봇 팔 궤적, 접촉 상태를 탐색할 수 있다. 최종 작업 자세를 선택할 때는 단순히 이동 거리만 최적화하는 것이 아니라 조작 도달 가능성, 가시성(Visibility), 안정성 여유(Stability Margin), 충돌 여유(Collision Clearance), 힘 생성 능력, 탈출 및 복구 가능성을 함께 고려해야 한다.

학습 기반 방법(Learning-Based Method)은 강하게 결합된 로코-매니퓰레이션 문제를 해결하기 위한 또 다른 접근법을 제공한다. 강화학습(Reinforcement Learning)은 수작업 규칙만으로 표현하기 어려운 다리, 몸체, 로봇 팔의 협조 동작을 최적화할 수 있으며, 모방학습(Imitation Learning)은 복잡한 상호작용 시퀀스의 시연을 정책으로 전달할 수 있다. 정책(Policy)은 고유수용성 상태, 지형 관측, 객체 정보, 작업 명령, 이전 행동 등을 입력으로 사용할 수 있다. 그러나 학습된 제어 역시 실제 배치 시 물리적 제약조건, 액추에이터 한계, 충돌 경계, 안전 요구사항을 준수해야 하며, 산업 설비나 사람 주변에서 작동할 경우 이러한 제약은 더욱 중요해진다.

실제 조작 대상은 이상적인 모델과 정확하게 일치하지 않기 때문에 강건성(Robustness)이 필수적이다. 객체 자세 추정에는 불확실성이 존재하고, 지형은 변형되거나 미끄러질 수 있으며, 파지 접촉점이 이동하거나 실제 상호작용력이 시뮬레이션과 달라질 수 있다. 따라서 실제 시스템은 개방루프 시퀀스(Open-Loop Sequence)에 의존하기보다 전체 작업 과정에서 피드백(Feedback)을 지속적으로 사용해야 한다. 파지 실패, 도달 불가능한 목표, 과도한 접촉력, 발 디딤 신뢰도 저하, 균형 악화 등이 발생하면 로봇 팔 후퇴, 지지 자세 확장, 몸체 재배치, 재인지(Re-Perception), 안전한 작업 종료와 같은 복구 행동(Recovery Behavior)을 수행해야 한다.

안전성(Safety)은 이동 계층과 조작 계층 전체에 걸쳐 적용되어야 한다. 관절 위치, 속도, 토크, 접촉력, 말단장치 속도 제한뿐만 아니라 안정성 및 충돌 제약조건도 함께 적용해야 한다. 로봇 팔 자체에는 안전한 조작 명령이라도 과도한 베이스 모멘트를 발생시키거나 발 디딤 안정성을 감소시킨다면 전체 로봇에는 위험할 수 있다. 마찬가지로 일반적으로 유효한 보행도 로봇 팔이 무거운 페이로드를 멀리 뻗어 들고 있는 상태에서는 위험해질 수 있다. 따라서 감독 로직(Supervisory Logic)은 결합된 전체 로봇 상태를 평가하고 제어 성능의 단계적 저하(Controlled Degradation), 보호 정지(Protective Stop), 자세 복구(Posture Recovery)를 제공해야 한다.

결과적으로 로봇 팔을 장착한 4족 보행 로봇은 단순히 보행 로봇에 매니퓰레이터를 추가한 시스템이 아니라 이동 가능한 물리적 상호작용 시스템(Mobile Physical Interaction System)으로 이해해야 한다. 실제 활용 능력은 협조된 인지, 지형 인식 기반 이동(Terrain-Aware Locomotion), 조작 계획, 전신 제어, 접촉 추론(Contact Reasoning), 학습, 안전 감독의 통합에서 발생한다. 이러한 관점은 이후 다루게 될 팔-베이스 협조, 검사 제어, 이동형 파지, 문과 밸브 조작, 페이로드 배치, 학습 기반 로코-매니퓰레이션, 동적 조작, 도구 사용, 산업 현장 적용을 이해하기 위한 기본 토대를 제공한다.

##  

## 09.02. Arm Base Coordination Whole Body Manip [w/Code]

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

Arm-base coordination enables an arm-equipped quadruped to treat its legs, floating base, and manipulator as one articulated system rather than as independently controlled subsystems. The objective is to distribute a manipulation task across all available degrees of freedom while maintaining stable ground contacts. A target end-effector pose may therefore be achieved through arm motion, trunk translation, trunk rotation, posture adjustment, or a coordinated combination of these motions.

The quadruped base differs fundamentally from the fixed base of a conventional industrial manipulator. Its trunk is supported through multiple unilateral foot contacts whose locations and allowable forces change with stance and gait. Consequently, movement of the arm modifies the load transmitted through the legs, while movement of the trunk changes the manipulator reference frame. Whole-body manipulation must continuously account for this coupling when calculating feasible joint motion and contact forces.

A useful mathematical representation defines a generalized configuration containing the floating-base pose, leg joint coordinates, and manipulator joint coordinates. The corresponding generalized velocity includes base linear and angular velocity together with all actuated joint velocities. Kinematic models then relate these variables to task-space quantities such as foot poses, center-of-mass motion, trunk orientation, elbow configuration, and end-effector position and orientation through their respective Jacobian matrices.

End-effector motion can be expressed relative to the world, trunk, or task frame depending on the manipulation objective. For precise interaction with an environmental object, a world- or object-referenced target is often preferable because the trunk may move while the hand should remain stationary. The controller must compensate for base motion by coordinating manipulator joints so that commanded end-effector motion remains consistent even when balance regulation causes small translations or rotations of the body.

Task hierarchy provides a practical mechanism for organizing competing whole-body objectives. Maintaining valid stance contacts and preventing loss of balance normally receive high priority, while end-effector tracking, trunk posture, joint configuration, and secondary optimization objectives are assigned compatible priorities. Rather than commanding every degree of freedom independently, the controller solves for a whole-body motion that satisfies critical constraints while exploiting remaining redundancy to improve manipulation performance.

Optimization-based whole-body control can formulate this coordination as a quadratic program. Decision variables may include generalized accelerations, joint torques, and contact forces. The optimization minimizes tracking errors for manipulation and posture tasks while satisfying rigid-body dynamics, stance-foot constraints, friction limits, torque bounds, and acceleration limits. This formulation allows manipulation objectives to be incorporated without violating the physical requirements needed to keep the quadruped standing safely.

Contact constraints are especially important because stance feet should remain approximately stationary relative to the supporting terrain during manipulation. Their velocities or accelerations can be constrained while contact forces are maintained inside feasible friction regions. If an arm motion generates a large reaction moment, the optimizer can redistribute ground reaction forces among the supporting legs. The robot can therefore counter manipulation disturbances using its complete support structure instead of relying only on arm joint control.

Redundancy resolution allows the system to use the quadruped body to extend the effective manipulator workspace. When the arm approaches a joint limit or poorly conditioned configuration, the trunk can translate, rotate, raise, or lower to restore a favorable arm posture. A secondary objective may keep joints near preferred configurations or maximize manipulability. This approach reduces unnecessary arm extension and can increase both positioning accuracy and available force at the end effector.

Manipulability is not determined only by the arm Jacobian because the floating base contributes additional motion capability. A whole-body Jacobian can describe how coordinated base and arm motion affects the end effector. However, base motion is constrained by leg reachability, support geometry, terrain, and contact stability. The practically available workspace is therefore a constrained whole-body workspace rather than the unconstrained geometric workspace obtained by simply combining arm and base degrees of freedom.

Center-of-mass regulation must be coordinated with manipulation because arm movement and payload motion shift the mass distribution of the robot. Extending the arm forward may require the trunk to move backward or ground reaction forces to change accordingly. With heavier payloads, the controller may lower the body or widen the effective support configuration before executing the manipulation. These compensating motions can be generated automatically as consequences of stability and posture objectives within the whole-body controller.

Forceful manipulation introduces an additional coupling between end-effector wrench and foot contact forces. When the robot pushes a door, pulls a handle, or rotates a valve, the environment applies an equal reaction wrench to the robot. The controller must determine whether the current stance can generate the opposing forces without foot slip, excessive joint torque, or loss of balance. Manipulation feasibility should therefore include force capability as well as conventional geometric reachability.

For contact interaction, the end-effector objective can combine motion tracking with compliant behavior. Impedance or force-control commands define how the hand should respond to contact, while the whole-body controller distributes the resulting wrench through the arm, trunk, and stance legs. This separation is useful because the manipulation layer can specify desired interaction behavior without explicitly determining every supporting joint torque, while the whole-body layer preserves dynamic consistency across the complete robot.

Arm-base coordination also requires collision-aware posture management. Moving the trunk to improve reach may bring the arm close to a leg, sensor mast, payload, or surrounding structure. Self-collision and environmental collision constraints should therefore be incorporated into planning or represented as inequality constraints and avoidance objectives. Joint limits, cable routing, actuator range, camera visibility, and manipulator singularities further reduce the set of theoretically possible whole-body configurations.

The controller must distinguish between continuous base adjustment and explicit locomotion. Small trunk motions can often be generated while the feet remain fixed, but larger workspace changes eventually exceed leg kinematic limits. At that point, the robot must relocate one or more feet or execute a walking maneuver. A supervisory coordinator can monitor reachability and determine whether the task should continue through stance manipulation, body repositioning, stepping, or complete locomotion to a new manipulation pose.

During stepping, manipulation becomes more difficult because the number and geometry of supporting contacts change. The arm may need to maintain an object pose while one leg swings, causing the remaining stance legs to absorb both locomotion and manipulation loads. Task priorities and allowable manipulation forces can be adjusted according to gait phase. For demanding operations, the robot may intentionally stop walking and establish a stable stance before applying significant end-effector forces.

State estimation quality directly affects arm-base coordination. Errors in trunk pose, joint position, foot contact state, or terrain orientation propagate into the estimated end-effector pose relative to the environment. Sensor fusion using inertial measurements, joint encoders, contact information, and external perception can provide a consistent estimate of the floating-base state. Accurate timestamping and coordinate transformations are particularly important when high-rate whole-body control and lower-rate perception operate together.

Real-time implementation typically separates high-rate dynamic stabilization from slower manipulation planning. A planner may generate desired hand trajectories, trunk references, and preferred configurations at moderate frequency, while the whole-body controller continuously resolves them against current contact and dynamic constraints. Low-level actuator controllers then execute joint torque or position commands at higher rates. This layered timing structure allows computationally expensive planning without sacrificing rapid stabilization against disturbances.

Constraint relaxation is necessary when all requested tasks cannot be satisfied simultaneously. A commanded hand pose may become incompatible with contact constraints, joint limits, or available torque. Instead of producing unstable commands, the controller can soften lower-priority objectives using slack variables or reduce manipulation speed and force. Critical constraints such as actuator protection, contact integrity, and collision avoidance should remain hard whenever possible, while less critical tracking objectives degrade gracefully.

Arm-base coordination should also expose meaningful status information to higher-level task logic. Metrics such as end-effector error, manipulability, stability margin, contact-force utilization, joint-limit proximity, and optimization feasibility can indicate whether the current manipulation configuration remains acceptable. A task executive can use these signals to request body repositioning, change the stance, replan the grasp, reduce interaction force, or terminate the action before the controller reaches a physically infeasible state.

Simulation provides an effective environment for developing whole-body manipulation because contact configurations, payloads, friction coefficients, sensor errors, and external forces can be varied systematically. Tests should include arm extension near workspace boundaries, heavy payload handling, force application from different directions, body repositioning, contact transitions, and unexpected disturbances. Hardware validation can then progress from stationary low-force manipulation toward coordinated stepping and increasingly dynamic interaction.

Effective arm-base coordination ultimately transforms the quadruped from a mobile platform carrying a robot arm into a unified whole-body manipulator. Locomotion supplies adaptable support and workspace mobility, the floating base contributes controllable positioning freedom, and the arm provides precise interaction capability. Whole-body optimization connects these functions through common kinematic, dynamic, contact, and safety constraints, allowing the robot to manipulate objects while continuously adapting its posture and support configuration.

팔-베이스 협조(Arm-Base Coordination)는 로봇 팔이 장착된 4족 보행 로봇이 다리, 부유 베이스(Floating Base), 매니퓰레이터(Manipulator)를 서로 독립적으로 제어되는 하위 시스템이 아니라 하나의 관절 시스템(Articulated System)으로 다룰 수 있도록 한다. 목표는 안정적인 지면 접촉을 유지하면서 조작 작업을 사용 가능한 모든 자유도(Degree of Freedom)에 분배하는 것이다. 따라서 목표 말단장치 자세(End-Effector Pose)는 로봇 팔의 움직임, 몸통의 병진, 몸통의 회전, 자세 조정 또는 이러한 움직임의 협조된 조합을 통해 달성할 수 있다.

4족 보행 로봇의 베이스(Base)는 기존 산업용 매니퓰레이터의 고정 베이스(Fixed Base)와 근본적으로 다르다. 몸통은 여러 개의 단방향 발 접촉(Unilateral Foot Contact)을 통해 지지되며, 접촉 위치와 허용 가능한 힘은 지지 자세와 보행 상태에 따라 변화한다. 따라서 로봇 팔의 움직임은 다리를 통해 전달되는 하중을 변화시키고, 몸통의 움직임은 매니퓰레이터의 기준 좌표계를 변화시킨다. 전신 조작(Whole-Body Manipulation)은 실행 가능한 관절 움직임과 접촉력을 계산할 때 이러한 결합 관계를 지속적으로 고려해야 한다.

유용한 수학적 표현은 부유 베이스 자세(Floating-Base Pose), 다리 관절 좌표, 매니퓰레이터 관절 좌표를 포함하는 일반화 구성(Generalized Configuration)을 정의하는 것이다. 이에 대응하는 일반화 속도(Generalized Velocity)는 베이스의 선속도와 각속도, 그리고 모든 구동 관절의 속도를 포함한다. 이후 기구학 모델(Kinematic Model)은 각각의 자코비안 행렬(Jacobian Matrix)을 통해 이러한 변수들을 발 자세, 질량중심 운동, 몸통 방향, 팔꿈치 구성, 말단장치 위치와 방향 등의 작업공간(Task Space) 변수와 연결한다.

말단장치의 움직임은 조작 목적에 따라 월드(World), 몸통(Trunk), 작업 좌표계(Task Frame)를 기준으로 표현할 수 있다. 환경에 존재하는 객체와 정밀하게 상호작용하는 경우에는 몸통이 움직이는 동안에도 손이 정지된 상태를 유지해야 할 수 있으므로 월드 또는 객체 기준 목표가 유리하다. 제어기는 균형 조절로 인해 몸체에 작은 병진이나 회전이 발생하더라도 명령된 말단장치 움직임이 일관되게 유지되도록 매니퓰레이터 관절을 협조하여 베이스 움직임을 보상해야 한다.

작업 계층(Task Hierarchy)은 서로 경쟁하는 전신 목표를 체계적으로 구성하기 위한 실용적인 방법을 제공한다. 유효한 지지 접촉 유지와 균형 상실 방지는 일반적으로 높은 우선순위를 가지며, 말단장치 추종, 몸통 자세, 관절 구성, 부가적인 최적화 목표에는 서로 호환되는 우선순위가 할당된다. 모든 자유도에 독립적으로 명령을 내리는 대신 제어기는 중요한 제약조건을 만족하면서 남아 있는 여유 자유도(Redundancy)를 활용하여 조작 성능을 향상시키는 전신 움직임을 계산한다.

최적화 기반 전신 제어(Optimization-Based Whole-Body Control)는 이러한 협조 문제를 이차계획법(Quadratic Program, QP)으로 구성할 수 있다. 결정 변수(Decision Variable)에는 일반화 가속도, 관절 토크, 접촉력이 포함될 수 있다. 최적화 과정에서는 강체 동역학(Rigid-Body Dynamics), 지지 발 제약조건, 마찰 한계, 토크 한계, 가속도 한계를 만족하면서 조작 및 자세 작업의 추종 오차를 최소화한다. 이러한 구성은 4족 보행 로봇을 안전하게 서 있게 하는 물리적 요구조건을 위반하지 않으면서 조작 목표를 통합할 수 있도록 한다.

접촉 제약조건(Contact Constraint)은 조작 중 지지 발이 지지 지형에 대해 거의 정지된 상태를 유지해야 하기 때문에 특히 중요하다. 접촉력이 실행 가능한 마찰 영역(Friction Region) 내부에 유지되는 동안 발의 속도 또는 가속도를 제한할 수 있다. 로봇 팔의 움직임이 큰 반력 모멘트(Reaction Moment)를 발생시키면 최적화기는 지지 다리 사이에서 지면 반력(Ground Reaction Force)을 재분배할 수 있다. 따라서 로봇은 로봇 팔의 관절 제어에만 의존하지 않고 전체 지지 구조를 사용하여 조작 외란을 상쇄할 수 있다.

여유 자유도 해석(Redundancy Resolution)을 이용하면 4족 보행 로봇의 몸체를 활용하여 매니퓰레이터의 유효 작업공간을 확장할 수 있다. 로봇 팔이 관절 한계나 조건이 좋지 않은 자세에 접근하면 몸통을 병진 또는 회전시키거나 높이거나 낮추어 유리한 로봇 팔 자세를 복원할 수 있다. 부가적인 목표를 통해 관절을 선호 자세 근처에 유지하거나 조작성(Manipulability)을 최대화할 수도 있다. 이러한 접근법은 불필요하게 로봇 팔을 최대한 뻗는 동작을 줄이고 말단장치의 위치 정확도와 사용 가능한 힘을 모두 향상시킬 수 있다.

조작성(Manipulability)은 부유 베이스가 추가적인 운동 능력을 제공하기 때문에 로봇 팔의 자코비안만으로 결정되지 않는다. 전신 자코비안(Whole-Body Jacobian)은 베이스와 로봇 팔의 협조된 움직임이 말단장치에 어떠한 영향을 미치는지 표현할 수 있다. 그러나 베이스 움직임은 다리의 도달 가능성, 지지 형상, 지형, 접촉 안정성에 의해 제한된다. 따라서 실제로 사용할 수 있는 작업공간은 로봇 팔과 베이스의 자유도를 단순히 결합하여 얻는 무제약 기하학적 작업공간이 아니라 제약된 전신 작업공간(Constrained Whole-Body Workspace)이다.

질량중심 조절(Center-of-Mass Regulation)은 로봇 팔과 페이로드의 움직임이 로봇의 질량 분포를 변화시키므로 조작 작업과 협조되어야 한다. 로봇 팔을 앞으로 뻗으면 몸통을 뒤로 이동시키거나 이에 맞추어 지면 반력을 변화시켜야 할 수 있다. 무거운 페이로드를 다루는 경우에는 조작을 수행하기 전에 몸체를 낮추거나 유효 지지 구성을 넓힐 수 있다. 이러한 보상 동작은 전신 제어기 내부의 안정성 및 자세 목표에 따라 자동으로 생성될 수 있다.

큰 힘을 요구하는 조작(Forceful Manipulation)은 말단장치 렌치(End-Effector Wrench)와 발 접촉력 사이에 추가적인 결합 관계를 만든다. 로봇이 문을 밀거나 손잡이를 당기거나 밸브를 회전시키면 환경은 로봇에 크기가 같고 방향이 반대인 반력 렌치를 가한다. 제어기는 현재 지지 자세가 발의 미끄러짐, 과도한 관절 토크, 균형 상실 없이 이러한 힘에 대응할 수 있는지 판단해야 한다. 따라서 조작 실행 가능성(Manipulation Feasibility)은 일반적인 기하학적 도달 가능성뿐만 아니라 힘 생성 능력(Force Capability)까지 포함해야 한다.

접촉 상호작용(Contact Interaction)을 위해 말단장치 목표는 운동 추종과 순응 동작(Compliant Behavior)을 결합할 수 있다. 임피던스 제어(Impedance Control) 또는 힘 제어(Force Control) 명령은 손이 접촉에 어떻게 반응해야 하는지를 정의하고, 전신 제어기는 이에 따라 발생하는 렌치(Wrench)를 로봇 팔, 몸통, 지지 다리에 분배한다. 이러한 분리는 조작 계층이 모든 지지 관절 토크를 직접 결정하지 않고도 원하는 상호작용 동작을 지정할 수 있게 하며, 전신 계층은 전체 로봇에 걸쳐 동역학적 일관성(Dynamic Consistency)을 유지할 수 있도록 한다.

팔-베이스 협조는 충돌 인식 자세 관리(Collision-Aware Posture Management)도 필요로 한다. 도달 범위를 개선하기 위해 몸통을 움직이면 로봇 팔이 다리, 센서 마스트(Sensor Mast), 페이로드 또는 주변 구조물에 가까워질 수 있다. 따라서 자기 충돌(Self-Collision)과 환경 충돌 제약조건을 계획 과정에 포함하거나 부등식 제약조건 및 회피 목표로 표현해야 한다. 관절 한계, 케이블 배선, 액추에이터 작동 범위, 카메라 가시성, 매니퓰레이터 특이점(Singularity) 역시 이론적으로 가능한 전신 자세의 범위를 추가로 제한한다.

제어기는 연속적인 베이스 조정(Continuous Base Adjustment)과 명시적인 이동(Explicit Locomotion)을 구분해야 한다. 작은 몸통 움직임은 발을 고정한 상태에서도 생성할 수 있지만, 더 큰 작업공간 변화가 요구되면 결국 다리의 기구학적 한계를 초과하게 된다. 이때 로봇은 하나 이상의 발을 재배치하거나 보행 동작을 수행해야 한다. 감독 협조기(Supervisory Coordinator)는 도달 가능성을 감시하고 작업을 지지 상태 조작, 몸체 재배치, 스테핑(Stepping), 또는 새로운 조작 자세로의 완전한 이동 중 어떤 방식으로 계속할 것인지 결정할 수 있다.

스테핑 과정에서는 지지 접촉의 개수와 형상이 변화하기 때문에 조작이 더욱 어려워진다. 한쪽 다리가 스윙(Swing)하는 동안 로봇 팔이 객체 자세를 유지해야 할 수 있으며, 이 경우 나머지 지지 다리가 이동과 조작에서 발생하는 하중을 동시에 흡수해야 한다. 작업 우선순위와 허용 가능한 조작력은 보행 위상(Gait Phase)에 따라 조정될 수 있다. 큰 힘이 필요한 작업에서는 로봇이 의도적으로 보행을 중지하고 안정적인 지지 자세를 형성한 후 상당한 크기의 말단장치 힘을 가하도록 할 수 있다.

상태 추정(State Estimation)의 품질은 팔-베이스 협조에 직접적인 영향을 준다. 몸통 자세, 관절 위치, 발 접촉 상태 또는 지형 방향의 오차는 환경을 기준으로 추정된 말단장치 자세에 전달된다. 관성 측정(Inertial Measurement), 관절 인코더(Joint Encoder), 접촉 정보, 외부 인지(External Perception)를 이용한 센서 융합(Sensor Fusion)은 일관된 부유 베이스 상태 추정을 제공할 수 있다. 특히 고속 전신 제어와 상대적으로 저속인 인지 시스템이 함께 작동할 때 정확한 타임스탬프(Timestamp)와 좌표 변환(Coordinate Transformation)이 중요하다.

실시간 구현(Real-Time Implementation)은 일반적으로 고주파 동역학 안정화와 상대적으로 느린 조작 계획을 분리한다. 계획기는 중간 수준의 주파수에서 원하는 손 궤적, 몸통 기준값, 선호 자세를 생성할 수 있으며, 전신 제어기는 현재 접촉 및 동역학 제약조건을 고려하여 이러한 목표를 지속적으로 조정한다. 이후 저수준 액추에이터 제어기는 더 높은 주파수에서 관절 토크 또는 위치 명령을 실행한다. 이러한 계층적 시간 구조는 계산량이 큰 계획 기능을 사용하면서도 외란에 대한 빠른 안정화 성능을 유지할 수 있게 한다.

모든 요청된 작업을 동시에 만족시킬 수 없는 경우에는 제약조건 완화(Constraint Relaxation)가 필요하다. 명령된 손 자세가 접촉 제약조건, 관절 한계 또는 사용 가능한 토크와 양립할 수 없는 상태가 될 수 있다. 불안정한 명령을 생성하는 대신 제어기는 슬랙 변수(Slack Variable)를 이용하여 낮은 우선순위의 목표를 완화하거나 조작 속도와 힘을 감소시킬 수 있다. 액추에이터 보호, 접촉 무결성(Contact Integrity), 충돌 회피와 같은 핵심 제약조건은 가능한 한 강성 제약조건(Hard Constraint)으로 유지하고, 중요도가 낮은 추종 목표는 점진적으로 성능이 저하되도록 구성하는 것이 바람직하다.

팔-베이스 협조 시스템은 상위 작업 로직이 활용할 수 있는 의미 있는 상태 정보도 제공해야 한다. 말단장치 오차, 조작성, 안정성 여유, 접촉력 사용률, 관절 한계 접근도, 최적화 실행 가능성(Optimization Feasibility) 등의 지표는 현재 조작 자세가 적절한 상태로 유지되고 있는지를 나타낼 수 있다. 작업 실행기(Task Executive)는 이러한 신호를 사용하여 몸체 재배치, 지지 자세 변경, 파지 재계획, 상호작용력 감소 또는 제어기가 물리적으로 실행 불가능한 상태에 도달하기 전에 작업 종료를 요청할 수 있다.

시뮬레이션(Simulation)은 접촉 구성, 페이로드, 마찰계수, 센서 오차, 외력을 체계적으로 변화시킬 수 있기 때문에 전신 조작을 개발하는 데 효과적인 환경을 제공한다. 시험에는 작업공간 경계 근처에서의 로봇 팔 확장, 무거운 페이로드 처리, 여러 방향에서의 힘 적용, 몸체 재배치, 접촉 전환, 예상하지 못한 외란 등을 포함할 수 있다. 이후 하드웨어 검증(Hardware Validation)은 정지 상태의 저하중 조작에서 시작하여 협조 스테핑과 점차 동적인 상호작용으로 확장할 수 있다.

효과적인 팔-베이스 협조는 궁극적으로 4족 보행 로봇을 단순히 로봇 팔을 운반하는 이동 플랫폼에서 하나의 통합된 전신 매니퓰레이터(Whole-Body Manipulator)로 변화시킨다. 이동 기능은 적응 가능한 지지와 작업공간 이동성을 제공하고, 부유 베이스는 제어 가능한 위치 조정 자유도를 제공하며, 로봇 팔은 정밀한 상호작용 능력을 제공한다. 전신 최적화(Whole-Body Optimization)는 이러한 기능을 공통된 기구학, 동역학, 접촉 및 안전 제약조건을 통해 연결함으로써 로봇이 자세와 지지 구성을 지속적으로 조정하면서 객체를 안정적으로 조작할 수 있도록 한다.

##  

## 09.03. Inspection Camera Arm Pan Tilt Control [w/Code]

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

Inspection camera manipulation extends a quadruped robot from a mobile observation platform into an actively positioned sensing system. By mounting a camera on a manipulator or articulated inspection arm, the robot can move the sensor independently of the trunk and place it near gauges, pipes, electrical panels, valves, structural joints, or confined spaces. Pan-tilt control then provides fine directional adjustment while locomotion and arm motion establish the larger inspection workspace.

The inspection system can be understood as a hierarchy of mobility ranges. Quadruped locomotion provides large-scale translation through the environment, body posture changes provide intermediate positioning, manipulator motion places the camera near the target, and pan-tilt joints perform precise optical alignment. Coordinating these stages avoids unnecessary robot motion because small changes in viewing direction can be handled by the camera mechanism instead of repositioning the complete arm or quadruped.

A camera inspection task should define more than a desired sensor position. The camera optical axis, target distance, viewing angle, image scale, field of view, and expected visibility determine whether the resulting observation is useful. A controller can therefore represent the objective as a desired camera pose or as visual constraints that keep the target near the image center while maintaining an appropriate stand-off distance and orientation for measurement or recognition.

Pan and tilt joints provide a compact mechanism for controlling the camera viewing direction. Pan typically rotates the optical system around an approximately vertical axis, while tilt changes elevation around a transverse axis. Joint encoders provide the angular state required to calculate the camera orientation relative to the arm. Mechanical limits, cable routing, sensor housing geometry, backlash, velocity limits, and acceleration limits must be included so that commanded viewing motions remain physically realizable.

Coordinate-frame management is essential because the camera is attached to a moving kinematic chain. Transformations may be maintained among the world, quadruped base, manipulator base, arm links, pan joint, tilt joint, and camera optical frame. When the robot changes posture or the arm moves, the camera pose in the world changes even if the pan-tilt angles remain fixed. Accurate forward kinematics therefore allows the controller to distinguish camera motion caused by the arm from motion commanded directly at the pan-tilt unit.

A target-tracking controller can convert the relative target direction into desired pan and tilt angles. When image-based feedback is available, the horizontal and vertical displacement of a detected feature from the image center can be used as the control error. Proportional or PID control can reduce this error by commanding angular velocity or position. Filtering is normally required because noisy detections can otherwise produce visible camera jitter and unnecessary actuator motion.

Visual servoing provides a more general framework when inspection targets move in the image because of body sway, arm movement, or locomotion. Image-based visual servoing directly regulates visual features, while position-based approaches estimate target geometry and calculate camera motion in Cartesian space. For quadrupeds, visual feedback is particularly useful because small trunk oscillations produced by gait or terrain compliance can disturb the camera even when the manipulator joints accurately follow their references.

Camera stabilization should distinguish slow viewpoint changes from high-frequency disturbances. The arm and pan-tilt mechanism can follow deliberate inspection trajectories, while inertial measurements can help compensate for faster angular disturbances. A filtered estimate of camera orientation or angular velocity can generate stabilization corrections. The achievable compensation bandwidth depends on actuator dynamics, structural stiffness, communication delay, camera exposure, and the update rates of the perception and control loops.

Arm and pan-tilt coordination can be formulated as a redundancy-resolution problem. Multiple combinations of arm configuration and camera angles may observe the same target. The controller can prefer solutions that keep pan and tilt near their central ranges, avoid arm singularities, maintain collision clearance, and preserve future viewing freedom. When the pan joint approaches its limit, for example, the arm or quadruped body can rotate gradually so that the camera mechanism returns toward a neutral configuration.

Inspection often requires maintaining a controlled stand-off distance. Moving too close can reduce usable field of view, cause focus problems, or create collision risk, while excessive distance can reduce spatial resolution. The manipulator can regulate camera position while pan-tilt control maintains orientation. Depth sensing, stereo vision, range measurements, or known target geometry may provide the distance estimate required to maintain a repeatable inspection viewpoint.

Collision avoidance is especially important when the camera is inserted near machinery or into narrow spaces. The planner must consider not only the camera housing but also the complete manipulator, cables, pan-tilt mechanism, and quadruped body. A viewing pose that produces an excellent image may be unacceptable if the elbow intersects a pipe or leaves insufficient clearance for stabilization motion. Collision-aware planning should therefore be performed together with visibility and camera-placement optimization.

Occlusion provides another constraint unique to inspection. A target may be geometrically reachable but hidden by equipment, the robot\'s own arm, or surrounding structures. Candidate viewpoints can be evaluated according to line of sight, expected target coverage, viewing incidence angle, and distance. If visibility deteriorates during execution, the system can modify pan-tilt orientation first, then reposition the arm, and finally relocate the quadruped when local adjustments cannot restore the required observation.

Automated inspection benefits from viewpoint sequencing rather than treating each image independently. A mission planner can specify a series of assets or regions to inspect, while a local camera planner determines suitable viewpoints for each target. The robot may stop at one base location and inspect several nearby components by moving only the arm and camera. This reduces locomotion time, energy consumption, terrain exposure, and positioning uncertainty compared with moving the complete robot for every observation.

Image acquisition should be synchronized with robot motion when measurement quality is important. Images captured during rapid arm movement or body vibration may suffer from motion blur or inconsistent viewpoints. The system can trigger acquisition after camera velocity falls below a threshold or when pose error enters a specified tolerance. Exposure time, illumination, autofocus state, thermal-camera integration time, and other sensor-specific conditions can also be incorporated into the capture decision.

Inspection payloads may contain more than a conventional RGB camera. Thermal imagers, zoom cameras, depth cameras, radiation sensors, acoustic sensors, or other instruments can share the articulated arm. Pan-tilt control then becomes part of a general sensor-pointing subsystem. Different sensors may require different stand-off distances and viewing orientations, so the inspection task should expose sensor-specific constraints while reusing common arm positioning, stabilization, collision avoidance, and target-tracking functions.

Zoom control can be coordinated with physical camera positioning when an optical zoom camera is used. Increasing focal length improves apparent target size but narrows the field of view and amplifies pointing errors and vibration. The system may first acquire the target using a wide field of view, center it through pan-tilt control, and then increase zoom gradually while tightening stabilization requirements. Loss of the target can trigger zoom reduction and reacquisition rather than uncontrolled searching.

Quadruped posture can improve camera access without requiring a full locomotion maneuver. Lowering the body may allow inspection beneath equipment, while raising or pitching the trunk can extend vertical reach. These posture changes must remain compatible with terrain contact and balance constraints. The inspection planner can therefore treat body pose as an additional sensing degree of freedom, but significant posture adjustment should remain coordinated with locomotion and whole-body control rather than being commanded solely by the camera subsystem.

During walking inspection, the camera controller must operate despite periodic base motion and changing foot contacts. A high-level target direction can remain fixed in the world while arm and pan-tilt commands compensate for trunk motion. However, stabilization authority is finite, and aggressive locomotion can exceed actuator bandwidth or produce excessive blur. Mission logic should therefore select walking speed and gait according to required image quality, using stationary inspection when high-resolution measurements are necessary.

Fault handling is required because inspection may occur in locations where direct human recovery is difficult. Loss of target detection, encoder faults, actuator saturation, communication delay, unexpected contact, or camera-stream failure should produce controlled responses. The system can freeze the current viewpoint, retract the arm, return the pan-tilt mechanism to a protected pose, or abort the inspection. Safe retraction paths are particularly important when the sensor has been inserted into confined machinery.

Performance evaluation should measure both robotic and sensing quality. Relevant quantities include pointing error, target-centering error, camera-pose repeatability, stabilization residual, tracking bandwidth, image sharpness, target visibility, inspection coverage, and time required to acquire each viewpoint. Tests should include stationary stance, body posture changes, arm repositioning, walking disturbances, different target distances, occlusions, low illumination, and narrow-space inspection to characterize practical operating limits.

An integrated inspection camera arm ultimately allows the quadruped to position perception actively rather than accepting whatever viewpoint is available from fixed body sensors. Locomotion determines where the robot can operate, whole-body posture establishes a useful support configuration, the arm determines sensor position, and pan-tilt control precisely directs the optical axis. Their coordinated operation enables repeatable, close-range inspection of assets that would otherwise be difficult, hazardous, or inaccessible to conventional mobile sensing platforms.

검사용 카메라 조작(Inspection Camera Manipulation)은 4족 보행 로봇을 단순한 이동형 관측 플랫폼(Mobile Observation Platform)에서 능동적으로 위치를 조정할 수 있는 센싱 시스템(Actively Positioned Sensing System)으로 확장한다. 카메라를 매니퓰레이터(Manipulator) 또는 관절형 검사 암(Articulated Inspection Arm)에 장착하면 로봇은 몸통과 독립적으로 센서를 움직여 계기판, 배관, 전기 패널, 밸브, 구조물 접합부 또는 협소 공간 가까이에 배치할 수 있다. 팬-틸트 제어(Pan-Tilt Control)는 세밀한 방향 조정을 담당하고, 이동과 로봇 팔 움직임은 더 넓은 검사 작업공간을 형성한다.

검사 시스템은 서로 다른 이동 범위를 갖는 계층 구조로 이해할 수 있다. 4족 보행 이동(Quadruped Locomotion)은 환경 내에서 대규모 병진 이동을 제공하고, 몸체 자세 변화는 중간 규모의 위치 조정을 수행하며, 매니퓰레이터 움직임은 카메라를 검사 대상 가까이에 배치한다. 이후 팬-틸트 관절은 정밀한 광학 정렬(Optical Alignment)을 수행한다. 이러한 단계들을 협조하면 작은 시선 방향 변화 때문에 전체 로봇 팔이나 4족 보행 로봇을 불필요하게 재배치하는 것을 방지할 수 있다.

카메라 검사 작업(Camera Inspection Task)은 단순히 원하는 센서 위치만 정의해서는 충분하지 않다. 카메라 광축(Optical Axis), 목표물과의 거리, 관측 각도, 영상 크기, 시야각(Field of View), 예상 가시성(Visibility)이 실제 관측 결과의 유용성을 결정한다. 따라서 제어기는 목표를 원하는 카메라 자세(Camera Pose)로 표현하거나, 측정 또는 인식에 적절한 이격 거리(Stand-Off Distance)와 방향을 유지하면서 검사 대상을 영상 중심 부근에 유지하도록 시각적 제약조건(Visual Constraint)으로 표현할 수 있다.

팬(Pan)과 틸트(Tilt) 관절은 카메라 시선 방향을 제어하기 위한 소형 메커니즘을 제공한다. 팬은 일반적으로 광학 시스템을 거의 수직인 축을 중심으로 회전시키며, 틸트는 횡방향 축을 중심으로 고도각을 변경한다. 관절 인코더(Joint Encoder)는 로봇 팔을 기준으로 카메라 방향을 계산하는 데 필요한 각도 상태를 제공한다. 명령된 시선 움직임이 물리적으로 실행 가능하도록 기계적 한계, 케이블 배선, 센서 하우징 형상, 백래시(Backlash), 속도 한계, 가속도 한계를 함께 고려해야 한다.

카메라는 움직이는 기구학적 체인(Kinematic Chain)에 부착되므로 좌표계 관리(Coordinate-Frame Management)가 필수적이다. 월드(World), 4족 보행 로봇 베이스, 매니퓰레이터 베이스, 로봇 팔 링크, 팬 관절, 틸트 관절, 카메라 광학 좌표계(Camera Optical Frame) 사이의 변환 관계를 유지할 수 있다. 로봇 자세가 변하거나 로봇 팔이 움직이면 팬-틸트 각도가 고정되어 있어도 월드 좌표계에서 카메라 자세는 변화한다. 따라서 정확한 순기구학(Forward Kinematics)을 통해 로봇 팔 움직임에 의해 발생한 카메라 운동과 팬-틸트 장치에서 직접 명령된 운동을 구분할 수 있어야 한다.

목표 추적 제어기(Target-Tracking Controller)는 상대적인 목표 방향을 원하는 팬 및 틸트 각도로 변환할 수 있다. 영상 기반 피드백(Image-Based Feedback)을 사용할 수 있는 경우 감지된 특징점이 영상 중심에서 벗어난 수평 및 수직 변위를 제어 오차로 사용할 수 있다. 비례 제어(Proportional Control) 또는 PID 제어(PID Control)는 각속도나 각도 위치를 명령하여 이러한 오차를 감소시킬 수 있다. 잡음이 많은 검출 결과가 카메라 떨림과 불필요한 액추에이터 움직임을 발생시키지 않도록 일반적으로 필터링(Filtering)이 필요하다.

시각 서보잉(Visual Servoing)은 몸체 흔들림, 로봇 팔 움직임 또는 이동으로 인해 검사 대상이 영상 안에서 움직일 때 보다 일반적인 제어 프레임워크를 제공한다. 영상 기반 시각 서보잉(Image-Based Visual Servoing)은 시각 특징을 직접 제어하며, 위치 기반 방법(Position-Based Method)은 목표물의 기하학적 상태를 추정하여 카테시안 공간(Cartesian Space)에서 카메라 움직임을 계산한다. 4족 보행 로봇에서는 보행이나 지형 순응으로 발생하는 작은 몸통 진동이 매니퓰레이터 관절의 정확한 기준 추종에도 카메라를 흔들 수 있기 때문에 시각 피드백이 특히 유용하다.

카메라 안정화(Camera Stabilization)는 느린 시점 변화와 고주파 외란(High-Frequency Disturbance)을 구분해야 한다. 로봇 팔과 팬-틸트 메커니즘은 의도된 검사 궤적을 추종하고, 관성 측정(Inertial Measurement)은 보다 빠른 각도 외란을 보상하는 데 활용할 수 있다. 필터링된 카메라 방향 또는 각속도 추정값을 이용하여 안정화 보정 명령을 생성할 수 있다. 실제 보상 대역폭(Compensation Bandwidth)은 액추에이터 동역학, 구조 강성, 통신 지연, 카메라 노출, 인지 및 제어 루프의 갱신 주파수에 의해 제한된다.

로봇 팔과 팬-틸트 협조(Arm and Pan-Tilt Coordination)는 여유 자유도 해석(Redundancy Resolution) 문제로 구성할 수 있다. 동일한 검사 대상을 관측할 수 있는 로봇 팔 자세와 카메라 각도의 조합은 여러 가지가 존재할 수 있다. 제어기는 팬과 틸트가 중앙 작동 범위 부근에 유지되고, 로봇 팔 특이점(Singularity)을 피하며, 충돌 여유를 확보하고, 이후의 시선 변경 자유도를 보존하는 해를 선호할 수 있다. 예를 들어 팬 관절이 작동 한계에 접근하면 로봇 팔이나 4족 보행 로봇 몸체를 점진적으로 회전시켜 카메라 메커니즘을 중립 위치로 복귀시킬 수 있다.

검사 작업에서는 제어된 이격 거리(Stand-Off Distance)를 유지해야 하는 경우가 많다. 카메라가 지나치게 가까워지면 사용 가능한 시야각이 감소하고 초점 문제가 발생하거나 충돌 위험이 증가할 수 있으며, 너무 멀어지면 공간 해상도(Spatial Resolution)가 감소할 수 있다. 매니퓰레이터는 카메라 위치를 조절하고 팬-틸트 제어는 카메라 방향을 유지할 수 있다. 깊이 센싱(Depth Sensing), 스테레오 비전(Stereo Vision), 거리 측정 또는 알려진 목표물 형상을 이용하여 반복 가능한 검사 시점을 유지하는 데 필요한 거리 정보를 얻을 수 있다.

카메라가 기계 설비 가까이에 삽입되거나 좁은 공간으로 진입하는 경우 충돌 회피(Collision Avoidance)는 특히 중요하다. 계획기는 카메라 하우징뿐만 아니라 전체 매니퓰레이터, 케이블, 팬-틸트 메커니즘, 4족 보행 로봇 몸체까지 고려해야 한다. 뛰어난 영상을 제공하는 시점이라도 로봇 팔꿈치가 배관과 충돌하거나 안정화 움직임을 위한 충분한 여유 공간을 확보하지 못한다면 사용할 수 없다. 따라서 충돌 인식 계획(Collision-Aware Planning)은 가시성 및 카메라 배치 최적화와 함께 수행되어야 한다.

가림(Occlusion)은 검사 작업에서 발생하는 또 다른 중요한 제약조건이다. 목표물이 기하학적으로 도달 가능한 위치에 있더라도 장비, 로봇 자신의 팔 또는 주변 구조물에 의해 가려질 수 있다. 후보 시점(Candidate Viewpoint)은 시선 경로(Line of Sight), 예상 목표물 포함 범위, 관측 입사각(Viewing Incidence Angle), 거리를 기준으로 평가할 수 있다. 작업 중 가시성이 저하되면 먼저 팬-틸트 방향을 조정하고, 다음으로 로봇 팔을 재배치하며, 이러한 국부 조정으로 필요한 관측 상태를 복원할 수 없는 경우 최종적으로 4족 보행 로봇 자체를 이동시킬 수 있다.

자동 검사(Automated Inspection)는 각각의 영상을 독립적으로 취급하기보다 시점 순서 계획(Viewpoint Sequencing)을 활용할 때 효율성이 높아진다. 임무 계획기(Mission Planner)는 검사해야 할 일련의 설비 또는 영역을 지정하고, 지역 카메라 계획기(Local Camera Planner)는 각 목표에 적합한 시점을 결정할 수 있다. 로봇은 하나의 베이스 위치에 정지한 상태에서 로봇 팔과 카메라만 움직여 주변의 여러 구성요소를 검사할 수 있다. 이는 모든 관측마다 전체 로봇을 이동시키는 방법보다 이동 시간, 에너지 소비, 지형 노출, 위치 불확실성을 줄일 수 있다.

측정 품질이 중요한 경우 영상 획득(Image Acquisition)은 로봇 움직임과 동기화되어야 한다. 빠른 로봇 팔 움직임이나 몸체 진동 중에 촬영된 영상에는 모션 블러(Motion Blur)가 발생하거나 시점이 일관되지 않을 수 있다. 시스템은 카메라 속도가 특정 임계값 이하로 감소하거나 자세 오차가 지정된 허용 범위에 들어온 이후 촬영을 트리거(Trigger)할 수 있다. 노출 시간, 조명 상태, 자동 초점 상태, 열화상 카메라 적분 시간(Thermal-Camera Integration Time) 등 센서별 조건도 촬영 판단에 포함할 수 있다.

검사용 페이로드(Inspection Payload)는 일반적인 RGB 카메라 이외의 센서를 포함할 수 있다. 열화상 카메라(Thermal Imager), 줌 카메라(Zoom Camera), 깊이 카메라(Depth Camera), 방사선 센서(Radiation Sensor), 음향 센서(Acoustic Sensor) 또는 기타 계측 장치를 동일한 관절형 로봇 팔에 탑재할 수 있다. 이 경우 팬-틸트 제어는 범용 센서 지향 시스템(Sensor-Pointing Subsystem)의 일부가 된다. 센서마다 요구되는 이격 거리와 관측 방향이 다를 수 있으므로 검사 작업은 센서별 제약조건을 제공하면서 공통적인 로봇 팔 위치 결정, 안정화, 충돌 회피, 목표 추적 기능을 재사용할 수 있어야 한다.

광학 줌 카메라(Optical Zoom Camera)를 사용하는 경우 줌 제어(Zoom Control)를 물리적인 카메라 위치 조정과 협조할 수 있다. 초점거리를 증가시키면 목표물의 영상 크기는 커지지만 시야각은 좁아지고 포인팅 오차(Pointing Error)와 진동의 영향은 확대된다. 시스템은 먼저 넓은 시야각으로 목표물을 획득하고 팬-틸트 제어를 통해 중앙에 정렬한 후, 안정화 요구조건을 강화하면서 점진적으로 줌을 증가시킬 수 있다. 목표물을 잃은 경우 무제어 탐색 대신 줌을 줄이고 목표물을 다시 획득하도록 구성할 수 있다.

4족 보행 로봇의 자세(Posture)는 완전한 이동 동작을 수행하지 않고도 카메라 접근성을 향상시킬 수 있다. 몸체를 낮추면 장비 아래쪽을 검사할 수 있고, 몸통을 높이거나 피치(Pitch)를 변경하면 수직 방향 도달 범위를 확장할 수 있다. 이러한 자세 변화는 지형 접촉 및 균형 제약조건과 양립해야 한다. 따라서 검사 계획기는 몸체 자세를 추가적인 센싱 자유도(Sensing Degree of Freedom)로 사용할 수 있지만, 큰 자세 변화는 카메라 하위 시스템에서 독립적으로 명령하기보다 이동 및 전신 제어와 협조하여 수행해야 한다.

보행 중 검사(Walking Inspection)에서는 주기적인 베이스 움직임과 변화하는 발 접촉 상태에도 카메라 제어기가 동작해야 한다. 상위 수준의 목표 방향은 월드 좌표계에서 고정된 상태로 유지하면서 로봇 팔과 팬-틸트 명령을 통해 몸통 움직임을 보상할 수 있다. 그러나 안정화 능력에는 한계가 있으며, 공격적인 이동은 액추에이터 대역폭을 초과하거나 과도한 영상 흐림을 발생시킬 수 있다. 따라서 임무 로직은 필요한 영상 품질에 따라 보행 속도와 보행 패턴(Gait)을 선택하고, 고해상도 측정이 필요한 경우 정지 상태 검사를 사용해야 한다.

직접적인 사람의 복구가 어려운 장소에서 검사가 수행될 수 있으므로 고장 처리(Fault Handling)가 필요하다. 목표물 검출 손실, 인코더 고장, 액추에이터 포화(Actuator Saturation), 통신 지연, 예상하지 못한 접촉, 카메라 스트림 장애 등이 발생하면 제어된 대응을 수행해야 한다. 시스템은 현재 시점을 고정하거나 로봇 팔을 후퇴시키고, 팬-틸트 메커니즘을 보호 자세로 복귀시키거나 검사를 중단할 수 있다. 특히 센서가 좁은 기계 구조 내부로 삽입된 경우에는 안전한 후퇴 경로(Safe Retraction Path)가 중요하다.

성능 평가(Performance Evaluation)는 로봇 성능과 센싱 품질을 모두 측정해야 한다. 관련 지표에는 포인팅 오차, 목표물 중심 정렬 오차, 카메라 자세 반복 정밀도, 안정화 잔류 오차(Stabilization Residual), 추적 대역폭, 영상 선명도, 목표물 가시성, 검사 범위, 각 시점을 획득하는 데 필요한 시간이 포함된다. 실제 운용 한계를 파악하기 위해 정지 지지 자세, 몸체 자세 변화, 로봇 팔 재배치, 보행 외란, 다양한 목표 거리, 가림, 저조도 환경, 협소 공간 검사 등을 포함하여 시험해야 한다.

통합된 검사용 카메라 암(Inspection Camera Arm)은 궁극적으로 4족 보행 로봇이 몸체에 고정된 센서에서 우연히 확보되는 시점에 의존하는 대신 인지 위치를 능동적으로 결정할 수 있도록 한다. 이동 기능은 로봇이 작업할 수 있는 위치를 결정하고, 전신 자세는 유용한 지지 구성을 형성하며, 로봇 팔은 센서의 위치를 결정하고, 팬-틸트 제어는 광축을 정밀하게 지향한다. 이러한 기능의 협조된 동작을 통해 기존 이동형 센싱 플랫폼으로는 접근하기 어렵거나 위험한 설비에 대해서도 반복 가능하고 정밀한 근거리 검사(Close-Range Inspection)를 수행할 수 있다.

##  

## 09.04. Object Pickup while Walking Mobile Grasp [w/Code]

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

Object pickup while walking combines quadruped locomotion, object perception, grasp planning, arm motion, and balance control into a continuous mobile manipulation task. Unlike conventional pick-and-place, the robot does not necessarily stop at a predefined manipulation pose before reaching for an object. It can approach the target while adjusting its body and manipulator, allowing locomotion to contribute directly to grasp acquisition and increasing the effective manipulation workspace.

The central challenge is that the grasp target is observed from a moving reference frame. Walking produces translation, rotation, vertical body motion, and periodic disturbances associated with changing foot contacts. Meanwhile, the target may remain stationary in the world or move independently. The perception and control system must therefore maintain a consistent estimate of object pose relative to the world, robot base, and manipulator while these coordinate frames continuously change.

Mobile grasping typically begins with target detection and localization at sufficient distance for approach planning. RGB, depth, stereo, or LiDAR perception can estimate object position, orientation, dimensions, and surrounding free space. The robot should also estimate whether the object is graspable from its current approach direction. Early perception allows locomotion to steer toward a region that provides favorable visibility, arm reachability, collision clearance, and stable footholds rather than simply minimizing walking distance.

A grasp candidate includes more than an end-effector pose. It should specify the approach direction, gripper orientation, finger configuration, clearance, expected contact region, and required object-relative motion. Candidate grasps can be evaluated together with the predicted robot configuration at pickup time. A grasp that is feasible from a stationary base may become unsuitable during walking because body oscillation, limited arm compensation, or reduced support geometry leaves insufficient tracking margin.

The pickup problem therefore requires prediction of both target state and robot motion. The controller can estimate where the quadruped base will be when the hand reaches the object and generate a corresponding arm trajectory. If the object is moving, its future pose must also be predicted. The grasp is then planned around an interception condition in which the hand and object reach compatible position, orientation, and relative velocity within an acceptable temporal window.

Locomotion and manipulation planning should exchange information continuously. The locomotion planner can modify walking velocity, heading, body height, or footholds to improve manipulation feasibility, while the arm planner reports workspace margins and preferred approach geometry. If the target lies near the edge of the arm workspace, a small change in body trajectory may provide substantially more robust grasping than extending the manipulator toward a singular or joint-limited configuration.

Walking phase strongly affects grasp feasibility. During phases with a larger or better distributed support region, the robot may tolerate greater arm acceleration and interaction force. During reduced-support phases, aggressive reaching can create undesirable angular momentum or shift the center of mass toward a stability boundary. The manipulation controller can therefore synchronize critical grasp events with favorable gait phases or temporarily modify gait timing as the hand approaches the target.

Whole-body control provides the mechanism for coordinating these competing objectives. End-effector tracking, trunk orientation, center-of-mass regulation, swing-leg motion, stance-foot constraints, and joint limits can be considered simultaneously. Instead of forcing the arm alone to reject base disturbances, the controller can distribute compensation across the trunk and available joints. This is particularly useful when the hand must remain accurately aligned with an object while the quadruped continues stepping.

Visual servoing can correct errors that remain after geometric planning. As the robot approaches the object, image measurements provide increasingly precise relative information and can compensate for localization drift or imperfect object models. The controller may use image-space target error, estimated Cartesian pose error, or a combination of both. Perception latency must be considered because delayed corrections can destabilize tracking when the robot and hand are moving rapidly.

The final approach should generally reduce relative hand-object velocity before contact. Even when the quadruped continues walking, the arm can move relative to the trunk so that the end effector approximately matches the object\'s world-frame velocity at grasp closure. For a stationary object, this means canceling much of the base motion through coordinated arm motion. Reducing relative velocity lowers impact, improves finger placement, and decreases the probability that the object will be pushed away before secure grasp formation.

Contact detection marks an important transition from reaching to load-bearing manipulation. Gripper motor current, finger position, tactile sensing, force-torque measurements, or visual cues can indicate whether contact has occurred. The controller should distinguish successful enclosure from accidental collision or partial contact. Closing force can then be regulated according to object properties while the whole-body controller prepares for the additional load that will be introduced when the object leaves its supporting surface.

The instant of lifting changes the dynamics of the complete robot. Object mass becomes part of the moving system, shifting the combined center of mass and increasing manipulator joint torque. If the payload estimate is uncertain, force or torque measurements can provide an online estimate after lift-off. The controller may reduce walking speed, alter body posture, modify footholds, or move the arm toward a more compact carrying configuration once the object has been securely acquired.

Grasp verification should occur before the robot commits to faster locomotion. Finger closure alone does not guarantee that the object is securely held. Tactile distribution, gripper force, object motion relative to the hand, visual confirmation, or small controlled test motions can provide evidence of grasp stability. If confidence is low, the robot can slow down, place the object back, adjust the grasp, or stop walking rather than allowing a weak grasp to become a dropped payload.

Collision avoidance must remain active throughout the pickup sequence. The planner must consider collisions between the arm and legs, the grasped object and robot body, and the entire system and surrounding environment. During walking, these relationships change continuously as legs swing and the trunk oscillates. The grasped object should be added to the collision model immediately after acquisition because its geometry can significantly alter safe arm configurations and available walking clearance.

Terrain introduces another coupling between mobility and grasping. Uneven ground can produce body orientation changes that disturb the approach trajectory, while poor footholds near the target may prevent the robot from maintaining a desirable pickup configuration. Terrain perception should therefore influence where and when grasping occurs. In difficult conditions, the robot may deliberately slow down, shorten steps, widen stance, or transition to stationary manipulation rather than attempting an unnecessarily dynamic pickup.

Dynamic pickup should not be treated as mandatory behavior. A robust system should select among continuous walking pickup, slowed walking, step-and-grasp, or complete stop-and-grasp according to task urgency, object properties, terrain, and uncertainty. Lightweight objects with large grasp regions may permit continuous acquisition, whereas fragile, heavy, small, or poorly localized objects may require a stable stance. This adaptive strategy provides useful mobility without sacrificing reliability.

Recovery behavior is essential because mobile grasping contains multiple opportunities for failure. The target may become occluded, move unexpectedly, leave the reachable workspace, or produce an invalid grasp. The robot should be able to cancel the reach, retract the arm, adjust its path, reacquire the object, and generate another grasp attempt. If contact destabilizes the robot, balance recovery and safe arm motion must take priority over preserving the manipulation attempt.

Real-time implementation benefits from separating planning and stabilization rates. Object detection and grasp planning may operate at moderate frequency, trajectory generation can update as the target estimate changes, and whole-body control executes at a much higher rate. Time synchronization is critical because a pose estimate associated with an old camera frame may correspond to a substantially different robot configuration by the time it reaches the controller during dynamic walking.

Safety constraints should bound end-effector speed, contact force, joint torque, body attitude, stability margin, and allowable payload behavior. A mobile grasp command should be rejected or degraded when predicted motion approaches collision, actuator, or balance limits. The robot may automatically decrease walking velocity as uncertainty increases. For operations near people, additional limits on arm velocity, gripper force, and approach direction are required because both the base and manipulator contribute to relative motion.

Simulation allows mobile grasping to be tested across walking speeds, gait phases, object locations, perception errors, payload masses, friction conditions, and terrain profiles. Evaluation should measure grasp success rate, pickup time, end-effector tracking error, object-relative velocity at contact, disturbance to locomotion, stability margin, and post-grasp payload retention. Hardware testing can progress from stationary pickup to slow walking and finally continuous dynamic acquisition.

Successful object pickup while walking demonstrates the fundamental value of loco-manipulation. The quadruped no longer treats locomotion as a separate stage that must finish before manipulation begins. Instead, walking changes the reachable workspace, body motion contributes to the approach, the arm compensates for locomotion, and whole-body control preserves stability throughout contact and lifting. The result is a robot capable of acquiring objects naturally while moving through complex environments.

보행 중 객체 픽업(Object Pickup while Walking)은 4족 보행 이동(Quadruped Locomotion), 객체 인지(Object Perception), 파지 계획(Grasp Planning), 로봇 팔 움직임(Arm Motion), 균형 제어(Balance Control)를 하나의 연속적인 이동 조작 작업(Mobile Manipulation Task)으로 결합한다. 기존의 픽앤플레이스(Pick-and-Place)와 달리 로봇은 객체를 잡기 전에 반드시 사전에 정의된 조작 자세에서 정지할 필요가 없다. 목표물에 접근하면서 몸체와 매니퓰레이터(Manipulator)를 동시에 조정할 수 있으므로 이동 자체가 파지 획득에 직접 기여하고 유효 조작 작업공간을 확장한다.

핵심적인 어려움은 움직이는 기준 좌표계(Moving Reference Frame)에서 파지 목표물을 관측한다는 점이다. 보행은 병진, 회전, 수직 방향 몸체 운동과 변화하는 발 접촉에 따른 주기적인 외란을 발생시킨다. 동시에 목표물은 월드(World) 좌표계에서 정지해 있거나 독립적으로 움직일 수 있다. 따라서 인지 및 제어 시스템은 이러한 좌표계가 지속적으로 변화하는 상황에서도 월드, 로봇 베이스, 매니퓰레이터를 기준으로 한 객체 자세(Object Pose)를 일관되게 추정해야 한다.

이동형 파지(Mobile Grasping)는 일반적으로 접근 계획을 수행할 수 있을 정도의 거리에서 목표물을 검출하고 위치를 추정하는 과정으로 시작한다. RGB, 깊이(Depth), 스테레오(Stereo), 라이다(LiDAR) 기반 인지를 이용하여 객체 위치, 방향, 크기와 주변 자유 공간을 추정할 수 있다. 또한 현재 접근 방향에서 객체를 파지할 수 있는지도 판단해야 한다. 조기 인지를 활용하면 단순히 보행 거리를 최소화하는 대신 우수한 가시성, 로봇 팔 도달 가능성, 충돌 여유, 안정적인 발 디딤 위치를 제공하는 영역으로 이동 경로를 설정할 수 있다.

파지 후보(Grasp Candidate)는 단순한 말단장치 자세(End-Effector Pose) 이상의 정보를 포함한다. 접근 방향, 그리퍼 방향, 손가락 구성, 충돌 여유, 예상 접촉 영역, 필요한 객체 상대 운동 등을 지정해야 한다. 후보 파지는 픽업 시점에 예상되는 로봇 자세와 함께 평가할 수 있다. 정지된 베이스에서는 실행 가능한 파지라도 보행 중에는 몸체 진동, 제한된 로봇 팔 보상 능력 또는 감소된 지지 형상으로 인해 충분한 추종 여유를 확보하지 못하여 부적합할 수 있다.

따라서 픽업 문제에서는 목표물 상태와 로봇 움직임을 모두 예측해야 한다. 제어기는 손이 객체에 도달하는 시점의 4족 보행 로봇 베이스 위치를 예측하고 이에 대응하는 로봇 팔 궤적을 생성할 수 있다. 객체가 움직이는 경우에는 객체의 미래 자세도 예측해야 한다. 이후 손과 객체가 허용 가능한 시간 구간 내에서 서로 호환되는 위치, 방향, 상대 속도에 도달하도록 인터셉션 조건(Interception Condition)을 중심으로 파지를 계획한다.

이동 계획(Locomotion Planning)과 조작 계획(Manipulation Planning)은 지속적으로 정보를 교환해야 한다. 이동 계획기는 조작 실행 가능성을 높이기 위해 보행 속도, 진행 방향, 몸체 높이 또는 발 디딤 위치를 변경할 수 있으며, 로봇 팔 계획기는 작업공간 여유와 선호 접근 형상을 제공한다. 목표물이 로봇 팔 작업공간 경계 부근에 있는 경우에는 매니퓰레이터를 특이점(Singularity)이나 관절 한계까지 뻗는 것보다 몸체 궤적을 조금 변경하는 것이 훨씬 강건한 파지를 제공할 수 있다.

보행 위상(Gait Phase)은 파지 실행 가능성에 큰 영향을 준다. 지지 영역이 더 넓거나 적절하게 분포된 위상에서는 로봇이 더 큰 로봇 팔 가속도와 상호작용력을 허용할 수 있다. 반대로 지지 영역이 감소하는 위상에서 공격적인 리칭(Reaching)을 수행하면 불필요한 각운동량을 발생시키거나 질량중심을 안정성 경계 가까이 이동시킬 수 있다. 따라서 조작 제어기는 중요한 파지 이벤트를 유리한 보행 위상과 동기화하거나 손이 목표물에 접근할 때 보행 타이밍 자체를 일시적으로 변경할 수 있다.

전신 제어(Whole-Body Control)는 이러한 서로 경쟁하는 목표를 협조하기 위한 핵심 메커니즘을 제공한다. 말단장치 추종, 몸통 방향, 질량중심 조절, 스윙 다리 움직임, 지지 발 제약조건, 관절 한계를 동시에 고려할 수 있다. 베이스에서 발생하는 외란을 로봇 팔만으로 보상하도록 강제하는 대신 제어기는 몸통과 사용 가능한 관절 전체에 보상 움직임을 분배할 수 있다. 이는 4족 보행 로봇이 계속 발을 움직이는 동안 손을 객체에 정확하게 정렬해야 하는 경우 특히 유용하다.

시각 서보잉(Visual Servoing)은 기하학적 계획 이후에도 남아 있는 오차를 보정할 수 있다. 로봇이 객체에 접근함에 따라 영상 측정값을 통해 더욱 정밀한 상대 정보를 얻을 수 있으며, 위치 추정 드리프트(Localization Drift)나 불완전한 객체 모델을 보상할 수 있다. 제어기는 영상 공간 목표 오차(Image-Space Target Error), 추정된 카테시안 자세 오차(Cartesian Pose Error) 또는 이 둘의 조합을 사용할 수 있다. 로봇과 손이 빠르게 움직이는 상황에서는 지연된 보정이 추종을 불안정하게 만들 수 있으므로 인지 지연(Perception Latency)을 반드시 고려해야 한다.

최종 접근(Final Approach) 과정에서는 일반적으로 접촉 전에 손과 객체 사이의 상대 속도를 감소시켜야 한다. 4족 보행 로봇이 계속 이동하는 경우에도 로봇 팔을 몸통에 대해 상대적으로 움직여 파지가 닫히는 순간 말단장치가 객체의 월드 좌표계 속도와 거의 일치하도록 만들 수 있다. 정지된 객체의 경우 이는 협조된 로봇 팔 움직임으로 베이스 운동의 상당 부분을 상쇄하는 것을 의미한다. 상대 속도를 줄이면 충격을 감소시키고 손가락 배치 정확도를 높이며 안정적인 파지가 형성되기 전에 객체를 밀어내는 가능성을 낮출 수 있다.

접촉 검출(Contact Detection)은 리칭 단계에서 하중을 지지하는 조작 단계로 전환되는 중요한 시점을 나타낸다. 그리퍼 모터 전류, 손가락 위치, 촉각 센싱(Tactile Sensing), 힘-토크 측정(Force-Torque Measurement), 시각적 단서를 이용하여 접촉 발생 여부를 판단할 수 있다. 제어기는 성공적인 객체 포획과 우발적인 충돌 또는 부분 접촉을 구분해야 한다. 이후 객체 특성에 따라 닫힘 힘(Closing Force)을 조절하는 동시에 전신 제어기는 객체가 지지면에서 떨어지는 순간 추가되는 하중에 대비해야 한다.

객체를 들어 올리는 순간 전체 로봇의 동역학이 변화한다. 객체 질량이 이동 시스템의 일부가 되면서 결합 질량중심(Combined Center of Mass)이 이동하고 매니퓰레이터 관절 토크도 증가한다. 페이로드 추정값이 불확실한 경우에는 들어 올린 이후 힘 또는 토크 측정값을 이용하여 온라인으로 질량을 추정할 수 있다. 객체를 안정적으로 획득한 이후에는 제어기가 보행 속도를 감소시키고 몸체 자세와 발 디딤 위치를 변경하거나 로봇 팔을 보다 안정적인 운반 자세로 이동시킬 수 있다.

로봇이 더 빠른 이동을 시작하기 전에 파지 검증(Grasp Verification)을 수행해야 한다. 손가락이 닫혔다는 사실만으로 객체가 안정적으로 잡혔다고 판단할 수는 없다. 촉각 분포, 그리퍼 힘, 손을 기준으로 한 객체 움직임, 시각적 확인 또는 작은 제어 시험 동작을 통해 파지 안정성을 확인할 수 있다. 신뢰도가 낮은 경우 로봇은 약한 파지 상태에서 객체를 떨어뜨리는 대신 속도를 줄이고, 객체를 다시 내려놓거나, 파지를 조정하거나, 보행을 중지할 수 있다.

충돌 회피(Collision Avoidance)는 전체 픽업 과정에서 지속적으로 활성화되어야 한다. 계획기는 로봇 팔과 다리 사이의 충돌, 파지된 객체와 로봇 몸체 사이의 충돌, 그리고 전체 시스템과 주변 환경 사이의 충돌을 모두 고려해야 한다. 보행 중에는 다리가 스윙하고 몸통이 진동하면서 이러한 관계가 지속적으로 변화한다. 객체를 획득한 직후에는 해당 객체의 형상이 안전한 로봇 팔 자세와 사용 가능한 보행 여유를 크게 변화시킬 수 있으므로 즉시 충돌 모델(Collision Model)에 추가해야 한다.

지형(Terrain)은 이동성과 파지 사이에 또 다른 결합 관계를 형성한다. 불규칙한 지면은 몸체 방향 변화를 발생시켜 접근 궤적을 교란할 수 있으며, 목표물 주변에 적절한 발 디딤 위치가 부족하면 원하는 픽업 자세를 유지하지 못할 수 있다. 따라서 지형 인지(Terrain Perception)는 파지를 수행할 위치와 시점에 영향을 주어야 한다. 어려운 조건에서는 불필요하게 동적인 픽업을 시도하기보다 의도적으로 속도를 줄이고, 보폭을 짧게 하며, 지지 자세를 넓히거나, 정지 조작(Stationary Manipulation)으로 전환할 수 있다.

동적 픽업(Dynamic Pickup)을 반드시 수행해야 하는 동작으로 취급해서는 안 된다. 강건한 시스템은 작업 긴급도, 객체 특성, 지형, 불확실성에 따라 연속 보행 픽업(Continuous Walking Pickup), 감속 보행, 스텝-앤드-그랩(Step-and-Grasp), 완전 정지 후 파지(Stop-and-Grasp) 중에서 적절한 방법을 선택해야 한다. 넓은 파지 영역을 가진 가벼운 객체는 연속적인 획득이 가능할 수 있지만, 깨지기 쉽거나 무겁고 작으며 위치 추정이 불확실한 객체는 안정적인 지지 자세를 필요로 할 수 있다. 이러한 적응형 전략은 신뢰성을 희생하지 않으면서 이동성을 활용할 수 있게 한다.

이동형 파지에는 여러 단계에서 실패 가능성이 존재하므로 복구 행동(Recovery Behavior)이 필수적이다. 목표물이 가려지거나 예상하지 못하게 움직이고, 도달 가능한 작업공간을 벗어나거나, 유효하지 않은 파지가 발생할 수 있다. 로봇은 리칭 동작을 취소하고 로봇 팔을 후퇴시키며, 이동 경로를 조정하고, 객체를 다시 인식한 후 새로운 파지 시도를 생성할 수 있어야 한다. 접촉으로 인해 로봇이 불안정해지는 경우에는 기존 조작 시도를 유지하는 것보다 균형 복구(Balance Recovery)와 안전한 로봇 팔 움직임이 우선되어야 한다.

실시간 구현(Real-Time Implementation)에서는 계획과 안정화의 실행 주파수를 분리하는 것이 효과적이다. 객체 검출과 파지 계획은 중간 수준의 주파수에서 동작하고, 목표물 추정이 변화함에 따라 궤적 생성을 갱신하며, 전신 제어는 훨씬 높은 주파수에서 실행될 수 있다. 동적 보행 중에는 오래된 카메라 프레임에 대응하는 자세 추정값이 제어기에 도달할 시점에는 로봇 자세가 크게 달라져 있을 수 있으므로 시간 동기화(Time Synchronization)가 특히 중요하다.

안전 제약조건(Safety Constraint)은 말단장치 속도, 접촉력, 관절 토크, 몸체 자세, 안정성 여유, 허용 가능한 페이로드 동작을 제한해야 한다. 예측된 움직임이 충돌, 액추에이터 또는 균형 한계에 접근하면 이동형 파지 명령을 거부하거나 성능을 낮추어 실행해야 한다. 불확실성이 증가하면 로봇이 자동으로 보행 속도를 감소시키도록 구성할 수도 있다. 사람 주변에서 작업하는 경우에는 베이스와 매니퓰레이터가 모두 상대 운동에 기여하므로 로봇 팔 속도, 그리퍼 힘, 접근 방향에 추가적인 제한이 필요하다.

시뮬레이션(Simulation)을 이용하면 다양한 보행 속도, 보행 위상, 객체 위치, 인지 오차, 페이로드 질량, 마찰 조건, 지형 프로파일에서 이동형 파지를 시험할 수 있다. 평가 지표에는 파지 성공률, 픽업 시간, 말단장치 추종 오차, 접촉 순간의 객체 상대 속도, 이동에 발생하는 외란, 안정성 여유, 파지 이후 페이로드 유지 성능 등이 포함될 수 있다. 하드웨어 시험(Hardware Testing)은 정지 상태 픽업에서 시작하여 저속 보행 픽업을 거쳐 최종적으로 연속적인 동적 객체 획득으로 단계적으로 확장할 수 있다.

보행 중 성공적인 객체 픽업은 로코-매니퓰레이션(Loco-Manipulation)의 근본적인 가치를 보여준다. 4족 보행 로봇은 더 이상 이동을 조작이 시작되기 전에 반드시 완료해야 하는 별도의 단계로 취급하지 않는다. 대신 보행을 통해 도달 가능한 작업공간을 변화시키고, 몸체 움직임을 접근 과정에 활용하며, 로봇 팔은 이동으로 발생하는 움직임을 보상하고, 전신 제어는 접촉과 객체 인양 과정 전체에서 안정성을 유지한다. 그 결과 로봇은 복잡한 환경을 이동하면서 자연스럽게 객체를 획득할 수 있는 통합적인 이동 조작 능력을 갖게 된다.

##  

## 09.05. Door Handle and Valve Manipulation [w/Code]

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Door-handle and valve manipulation are representative contact-rich tasks for arm-equipped quadrupeds because they combine precise perception, constrained end-effector motion, sustained interaction force, and whole-body stability. Unlike free-space reaching, the robot becomes mechanically coupled to the environment after contact. Successful execution therefore requires coordinated control of the gripper, manipulator, floating base, supporting legs, and contact forces throughout the interaction.

The task begins with identifying the interaction mechanism and estimating its geometry. For a door, relevant quantities include handle position, handle orientation, hinge location, door plane, and expected opening direction. For a valve, the system should estimate the wheel or lever center, rotation axis, radius, graspable regions, and surrounding clearance. These estimates define both the initial grasp pose and the constrained motion that must follow after contact.

Perception uncertainty is particularly important because small pose errors can cause failed grasping or excessive contact force. RGB-D cameras, stereo vision, LiDAR, wrist cameras, or learned object detectors can provide an initial target estimate, while close-range sensing refines the pose during approach. Visual servoing can correct residual alignment error by continuously adjusting the end-effector trajectory relative to the detected handle or valve before physical contact occurs.

The quadruped should select a base pose that supports both geometric reachability and force generation. Standing too far away can force the arm near full extension, reducing manipulability and available interaction force. Standing too close may create self-collision or prevent the door from moving. The preferred stance should provide sufficient arm workspace, stable footholds, collision clearance, useful camera visibility, and a support geometry capable of resisting the expected reaction wrench.

Grasp planning depends strongly on the mechanism being operated. A lever-style door handle may require the gripper to approach from a particular direction, close around the handle, and rotate it before pulling or pushing the door. A round valve wheel may permit several grasp locations around its circumference. The selected grasp should maximize contact security while preserving enough manipulator workspace to execute the subsequent constrained trajectory without encountering joint limits.

After grasp establishment, the control problem changes from free-space manipulation to constrained interaction. The hand can no longer follow an arbitrary Cartesian trajectory because its motion is determined partly by the mechanism geometry. A door handle may rotate around its local axis, a door panel rotates around a hinge, and a valve follows a circular trajectory around a fixed shaft. The controller should represent these kinematic constraints explicitly or estimate them online from measured motion and force.

Force and torque sensing provides important feedback during mechanism operation. The robot can detect whether a handle is locked, whether a valve requires unexpectedly high torque, or whether the grasp is slipping. Excessive resistance should not simply produce increasing actuator effort. Instead, force thresholds and compliance behavior can prevent damage to the robot, mechanism, or environment while providing information that higher-level logic can use to classify the interaction state.

Impedance control is well suited to these tasks because exact mechanism geometry may not be known. Rather than enforcing a perfectly rigid position trajectory, the controller defines a desired relationship between position error and interaction wrench. Compliance can be permitted along uncertain directions while sufficient stiffness is maintained for grasp stability and task execution. This allows the end effector to follow small geometric deviations without generating unnecessarily large internal forces.

Hybrid motion-force control provides another useful formulation. Motion can be controlled along directions where the mechanism should move, while force is regulated along constrained directions. During valve rotation, for example, tangential motion may drive the wheel while radial contact force maintains engagement. During door opening, the controller can regulate the force applied normal to the handle or door while commanding the motion needed to follow the hinge-generated arc.

Whole-body coordination becomes necessary when reaction forces exceed what the arm alone can comfortably manage. Pulling a heavy door creates a wrench that propagates through the manipulator into the quadruped trunk and stance legs. The whole-body controller can modify trunk posture and redistribute ground reaction forces to oppose this disturbance. If necessary, the robot can widen its stance, lower its body, or select footholds that provide a more favorable support configuration before continuing.

Door opening introduces a changing workspace problem because the grasped handle moves as the door rotates. A base pose that is suitable at the beginning may become unsuitable later in the trajectory. The quadruped may therefore need to reposition its trunk or step while maintaining the grasp. Arm-base coordination should preserve the end-effector constraint while the legs establish a new support configuration, effectively turning door opening into a combined locomotion and manipulation problem.

Maintaining grasp during stepping requires careful task prioritization. The end effector should follow the door trajectory while stance contacts and balance constraints remain satisfied. When one leg swings, the remaining contacts must support both the robot and interaction wrench. The controller may reduce door-opening speed during contact transitions or temporarily pause mechanism motion while completing a step. This avoids forcing manipulation performance at the expense of locomotion stability.

Valve manipulation often requires repeated regrasping because the manipulator may not be able to rotate continuously through the full required angle. The robot can rotate the valve through the available arm range, stop while maintaining mechanism state, release the gripper, move to another grasp location, and continue rotation. Planning should ensure that each regrasp remains collision-free and that the valve does not unintentionally return due to stored mechanical force or process pressure.

A valve may also require substantial torque. The achievable end-effector wrench depends on manipulator configuration, actuator limits, grasp geometry, and quadruped support conditions. A configuration near a kinematic singularity may provide poor torque capability even when the valve is geometrically reachable. The planner should therefore consider force manipulability and predicted joint torque, selecting body and arm configurations that provide sufficient mechanical advantage for the expected operation.

Slip detection is important for both handles and valves. Relative motion between the gripper and mechanism can be inferred from tactile sensors, force changes, finger displacement, or visual tracking. When slip is detected, the controller can increase gripping force within safe limits, reduce manipulation speed, modify wrist orientation, or stop and regrasp. Continuing an operation with an unstable grasp can produce sudden loss of load and destabilize the entire quadruped.

State estimation should track the mechanism as the task progresses. Door angle, handle state, valve rotation angle, grasp condition, interaction wrench, and robot configuration together describe task progress. These variables allow the task executive to distinguish successful motion from situations in which the arm moves but the mechanism does not. Explicit state tracking also supports recovery because the robot can determine whether it should retry the grasp, increase force, reposition, or terminate the operation.

Task sequencing is naturally represented as a state machine or behavior tree. A door task may include detection, approach, pre-grasp alignment, grasp closure, handle actuation, latch verification, door motion, body repositioning, release, and passage. Valve operation may include detection, grasping, torque application, rotation monitoring, regrasping, completion verification, and release. Transitions should depend on sensed physical conditions rather than elapsed time alone.

Collision checking must account for the changing geometry of the environment. As a door opens, the door panel sweeps through space and may collide with the robot body, legs, or arm. Valve environments can contain nearby pipes, frames, or instrumentation that restrict wrist motion. Planning should update collision geometry according to estimated mechanism state so that trajectories remain safe throughout the interaction rather than only at the initial configuration.

Recovery strategies should be designed explicitly because contact-rich tasks frequently violate nominal assumptions. The robot may miss the handle, encounter a locked door, underestimate valve torque, lose visual tracking, or reach a joint limit during operation. Recovery can include releasing contact, retracting the arm, changing base position, selecting another grasp, re-estimating mechanism geometry, or requesting operator assistance instead of repeatedly applying uncontrolled force.

Safety supervision should limit gripper force, end-effector wrench, joint torque, body attitude, contact-force utilization, and mechanism speed. Unexpected force growth can indicate collision, jamming, or incorrect geometric estimation. Safety logic should be able to stop commanded motion while preserving a stable stance and, when appropriate, maintain or release the grasp in a controlled manner. Human proximity requires additional limits on door motion and manipulator velocity.

Simulation can evaluate variations in handle geometry, hinge location, valve size, friction, stiffness, required torque, perception error, and foothold conditions before hardware deployment. Useful metrics include grasp success, mechanism completion rate, peak interaction force, valve torque capability, door-opening time, number of regrasps, stability margin, and recovery success. Hardware testing should progress from low-force fixtures to realistic industrial mechanisms and constrained environments.

Door-handle and valve manipulation demonstrate why quadruped manipulation must integrate perception, contact control, force reasoning, and locomotion. The arm provides precise interaction, but successful operation depends on how the complete robot supports and reacts to environmental forces. By coordinating grasping, compliant control, whole-body stabilization, stepping, and recovery, an arm-equipped quadruped can operate mechanisms designed for humans while maintaining mobility across complex industrial environments.

문손잡이 및 밸브 조작(Door-Handle and Valve Manipulation)은 정밀한 인지(Perception), 제약된 말단장치 운동(Constrained End-Effector Motion), 지속적인 상호작용력(Interaction Force), 전신 안정성(Whole-Body Stability)을 결합하기 때문에 로봇 팔을 장착한 4족 보행 로봇의 대표적인 접촉 중심 작업(Contact-Rich Task)이다. 자유공간 리칭(Free-Space Reaching)과 달리 접촉 이후에는 로봇이 환경과 기계적으로 결합된다. 따라서 성공적인 작업을 위해서는 전체 상호작용 과정에서 그리퍼, 매니퓰레이터(Manipulator), 부유 베이스(Floating Base), 지지 다리, 접촉력을 협조하여 제어해야 한다.

작업은 상호작용 메커니즘(Interaction Mechanism)을 식별하고 그 기하학적 형상을 추정하는 것에서 시작한다. 문의 경우 손잡이 위치, 손잡이 방향, 힌지 위치, 문 평면, 예상 개방 방향 등이 중요한 정보가 된다. 밸브의 경우에는 휠 또는 레버의 중심, 회전축, 반경, 파지 가능한 영역, 주변 여유 공간을 추정해야 한다. 이러한 추정값은 초기 파지 자세뿐만 아니라 접촉 이후 수행해야 하는 제약 운동(Constrained Motion)을 정의한다.

작은 자세 오차도 파지 실패나 과도한 접촉력을 발생시킬 수 있으므로 인지 불확실성(Perception Uncertainty)은 특히 중요하다. RGB-D 카메라, 스테레오 비전(Stereo Vision), 라이다(LiDAR), 손목 카메라(Wrist Camera), 학습 기반 객체 검출기(Learned Object Detector)를 이용하여 초기 목표 자세를 추정하고, 근거리 센싱을 통해 접근 과정에서 자세를 정밀하게 보정할 수 있다. 시각 서보잉(Visual Servoing)은 물리적 접촉 전에 검출된 손잡이나 밸브를 기준으로 말단장치 궤적을 지속적으로 조정하여 잔여 정렬 오차를 보정할 수 있다.

4족 보행 로봇은 기하학적 도달 가능성(Geometric Reachability)과 힘 생성 능력(Force Generation)을 모두 지원할 수 있는 베이스 자세(Base Pose)를 선택해야 한다. 너무 멀리 서면 로봇 팔을 최대한 뻗어야 하므로 조작성(Manipulability)과 사용 가능한 상호작용력이 감소할 수 있다. 반대로 너무 가까우면 자기 충돌(Self-Collision)이 발생하거나 문이 움직일 공간을 확보하지 못할 수 있다. 적절한 지지 자세는 충분한 로봇 팔 작업공간, 안정적인 발 디딤, 충돌 여유, 카메라 가시성, 예상 반력 렌치(Reaction Wrench)를 견딜 수 있는 지지 형상을 제공해야 한다.

파지 계획(Grasp Planning)은 조작해야 하는 메커니즘의 종류에 크게 의존한다. 레버형 문손잡이(Lever-Style Door Handle)는 특정 방향에서 그리퍼가 접근하여 손잡이를 감싸고 닫은 후, 문을 밀거나 당기기 전에 손잡이를 회전시켜야 할 수 있다. 원형 밸브 휠(Round Valve Wheel)은 원주 주변의 여러 위치에서 파지할 수 있다. 선택된 파지는 안정적인 접촉을 최대화하는 동시에 이후의 제약 궤적을 관절 한계 없이 수행할 수 있도록 충분한 매니퓰레이터 작업공간을 확보해야 한다.

파지가 형성된 이후 제어 문제는 자유공간 조작에서 제약된 상호작용(Constrained Interaction)으로 변화한다. 손의 움직임은 메커니즘의 기하학적 구조에 의해 부분적으로 결정되므로 임의의 카테시안 궤적(Cartesian Trajectory)을 추종할 수 없다. 문손잡이는 자체 축을 중심으로 회전하고, 문 패널은 힌지를 중심으로 회전하며, 밸브는 고정된 축을 중심으로 원형 궤적을 따른다. 제어기는 이러한 기구학적 제약조건(Kinematic Constraint)을 명시적으로 표현하거나 측정된 움직임과 힘을 이용하여 온라인으로 추정해야 한다.

힘 및 토크 센싱(Force and Torque Sensing)은 메커니즘 조작 과정에서 중요한 피드백을 제공한다. 로봇은 손잡이가 잠겨 있는지, 밸브 회전에 예상보다 큰 토크가 필요한지, 또는 파지가 미끄러지고 있는지를 감지할 수 있다. 과도한 저항이 발생한다고 해서 단순히 액추에이터 출력을 계속 증가시켜서는 안 된다. 대신 힘 임계값과 순응 동작(Compliance Behavior)을 적용하여 로봇, 메커니즘, 주변 환경의 손상을 방지하고 상위 작업 로직이 상호작용 상태를 판단할 수 있는 정보를 제공해야 한다.

임피던스 제어(Impedance Control)는 정확한 메커니즘 형상을 알 수 없는 경우가 많기 때문에 이러한 작업에 적합하다. 완전히 강체적인 위치 궤적을 강제하는 대신 제어기는 위치 오차와 상호작용 렌치 사이의 원하는 관계를 정의한다. 불확실한 방향에는 순응성(Compliance)을 허용하면서 파지 안정성과 작업 수행에 필요한 방향에는 충분한 강성(Stiffness)을 유지할 수 있다. 이를 통해 말단장치는 작은 기하학적 오차를 따라 자연스럽게 움직이면서 불필요하게 큰 내부 힘이 발생하는 것을 방지할 수 있다.

하이브리드 운동-힘 제어(Hybrid Motion-Force Control) 역시 유용한 제어 구조를 제공한다. 메커니즘이 움직여야 하는 방향에서는 운동을 제어하고, 구속된 방향에서는 힘을 조절할 수 있다. 예를 들어 밸브를 회전할 때 접선 방향 운동(Tangential Motion)을 이용하여 휠을 회전시키고 방사 방향 접촉력(Radial Contact Force)을 조절하여 안정적인 접촉을 유지할 수 있다. 문을 열 때에는 힌지에 의해 형성되는 원호를 따라 필요한 움직임을 명령하면서 손잡이나 문에 수직한 방향으로 가해지는 힘을 조절할 수 있다.

반력이 로봇 팔만으로 안정적으로 처리할 수 있는 수준을 초과하면 전신 협조(Whole-Body Coordination)가 필요하다. 무거운 문을 당기면 매니퓰레이터를 통해 4족 보행 로봇의 몸통과 지지 다리로 렌치가 전달된다. 전신 제어기(Whole-Body Controller)는 몸통 자세를 변경하고 지면 반력(Ground Reaction Force)을 재분배하여 이러한 외란에 대응할 수 있다. 필요한 경우 로봇은 작업을 계속하기 전에 지지 자세를 넓히고, 몸체를 낮추거나, 더욱 유리한 지지 형상을 제공하는 발 디딤 위치를 선택할 수 있다.

문을 여는 작업에서는 문이 회전하면서 파지된 손잡이의 위치가 계속 변화하기 때문에 작업공간 문제도 동적으로 변화한다. 초기에는 적합했던 베이스 자세가 작업 후반에는 적절하지 않을 수 있다. 따라서 4족 보행 로봇은 파지를 유지하면서 몸통을 재배치하거나 발을 움직여야 할 수 있다. 팔-베이스 협조(Arm-Base Coordination)는 다리가 새로운 지지 구성을 형성하는 동안 말단장치의 제약조건을 유지해야 하며, 이를 통해 문 열기 작업은 이동과 조작이 결합된 문제로 확장된다.

스테핑(Stepping) 중 파지를 유지하려면 작업 우선순위를 세밀하게 관리해야 한다. 말단장치는 문의 궤적을 추종하는 동시에 지지 접촉과 균형 제약조건을 만족해야 한다. 한쪽 다리가 스윙(Swing)하는 동안에는 나머지 지지점들이 로봇 자체의 하중과 상호작용 렌치를 동시에 지지해야 한다. 제어기는 접촉 전환 과정에서 문을 여는 속도를 감소시키거나 스텝을 완료할 때까지 메커니즘의 움직임을 일시적으로 정지시킬 수 있다. 이를 통해 이동 안정성을 희생하면서 조작 성능을 강제하는 상황을 방지할 수 있다.

밸브 조작(Valve Manipulation)은 매니퓰레이터가 필요한 전체 회전각을 한 번의 동작으로 수행하지 못할 수 있기 때문에 반복적인 재파지(Regrasping)가 필요한 경우가 많다. 로봇은 사용 가능한 로봇 팔 작업 범위까지 밸브를 회전하고, 메커니즘 상태를 유지한 채 정지한 후 그리퍼를 해제하고 새로운 파지 위치로 이동하여 회전을 계속할 수 있다. 각 재파지 동작은 충돌 없이 수행되어야 하며, 저장된 기계적 힘이나 공정 압력(Process Pressure)에 의해 밸브가 의도하지 않게 되돌아가지 않도록 계획해야 한다.

밸브는 상당한 크기의 토크를 요구할 수도 있다. 사용 가능한 말단장치 렌치는 매니퓰레이터 자세, 액추에이터 한계, 파지 형상, 4족 보행 로봇의 지지 조건에 의해 결정된다. 기구학적 특이점(Kinematic Singularity) 부근의 자세는 밸브에 기하학적으로 도달할 수 있더라도 충분한 토크 생성 능력을 제공하지 못할 수 있다. 따라서 계획기는 힘 조작성(Force Manipulability)과 예상 관절 토크를 고려하여 필요한 작업에 충분한 기계적 이점(Mechanical Advantage)을 제공하는 몸체 및 로봇 팔 자세를 선택해야 한다.

미끄러짐 검출(Slip Detection)은 문손잡이와 밸브 모두에서 중요하다. 그리퍼와 메커니즘 사이의 상대 운동은 촉각 센서(Tactile Sensor), 힘 변화, 손가락 변위 또는 시각 추적을 통해 추정할 수 있다. 미끄러짐이 감지되면 제어기는 안전 한계 내에서 파지력을 증가시키고, 조작 속도를 감소시키거나, 손목 방향을 변경하거나, 작업을 중지하고 다시 파지할 수 있다. 불안정한 파지 상태에서 작업을 계속하면 갑작스러운 하중 상실이 발생하여 4족 보행 로봇 전체가 불안정해질 수 있다.

상태 추정(State Estimation)은 작업 진행 과정에서 메커니즘 상태를 지속적으로 추적해야 한다. 문 각도, 손잡이 상태, 밸브 회전각, 파지 상태, 상호작용 렌치, 로봇 자세를 함께 이용하여 작업 진행 상태를 표현할 수 있다. 이러한 변수들을 이용하면 로봇 팔은 움직이고 있지만 실제 메커니즘은 움직이지 않는 상황과 정상적인 작업 진행을 구분할 수 있다. 명시적인 상태 추적은 로봇이 파지를 다시 시도할지, 힘을 증가시킬지, 위치를 재조정할지 또는 작업을 종료할지를 판단하는 복구 과정에도 활용된다.

작업 순서(Task Sequencing)는 상태 머신(State Machine) 또는 행동 트리(Behavior Tree)를 이용하여 자연스럽게 표현할 수 있다. 문 조작 작업은 검출, 접근, 파지 전 정렬, 파지 폐쇄, 손잡이 작동, 래치 확인, 문 이동, 몸체 재배치, 해제, 통과 등의 단계로 구성할 수 있다. 밸브 조작은 검출, 파지, 토크 적용, 회전 감시, 재파지, 완료 확인, 해제 과정으로 구성할 수 있다. 각 단계의 전환은 단순한 경과 시간이 아니라 센서를 통해 확인된 실제 물리 상태를 기준으로 결정해야 한다.

충돌 검사(Collision Checking)는 환경의 변화하는 기하학적 구조를 고려해야 한다. 문이 열리면 문 패널이 공간을 회전하며 지나가므로 로봇 몸체, 다리 또는 로봇 팔과 충돌할 수 있다. 밸브 주변에는 배관, 프레임 또는 계측 장치가 존재하여 손목 움직임을 제한할 수 있다. 따라서 계획 시스템은 추정된 메커니즘 상태에 따라 충돌 형상을 갱신하여 초기 자세뿐만 아니라 전체 상호작용 과정에서 궤적이 안전하게 유지되도록 해야 한다.

접촉 중심 작업에서는 정상적인 가정이 쉽게 깨질 수 있으므로 복구 전략(Recovery Strategy)을 명시적으로 설계해야 한다. 로봇이 손잡이를 놓치거나, 잠긴 문을 만나거나, 밸브 토크를 과소평가하거나, 시각 추적을 잃거나, 작업 중 관절 한계에 도달할 수 있다. 이러한 경우 반복적으로 제어되지 않은 힘을 가하는 대신 접촉 해제, 로봇 팔 후퇴, 베이스 위치 변경, 다른 파지 선택, 메커니즘 형상 재추정 또는 작업자 지원 요청 등의 복구 동작을 수행할 수 있어야 한다.

안전 감독(Safety Supervision)은 그리퍼 힘, 말단장치 렌치, 관절 토크, 몸체 자세, 접촉력 사용률, 메커니즘 작동 속도를 제한해야 한다. 예상하지 못한 힘의 증가는 충돌, 걸림(Jamming) 또는 잘못된 기하학적 추정을 의미할 수 있다. 안전 로직은 안정적인 지지 자세를 유지하면서 명령된 움직임을 중지할 수 있어야 하며, 필요한 경우 파지를 제어된 방식으로 유지하거나 해제해야 한다. 사람과 가까운 환경에서는 문 움직임과 매니퓰레이터 속도에도 추가적인 제한을 적용해야 한다.

시뮬레이션(Simulation)을 이용하면 하드웨어 배치 전에 손잡이 형상, 힌지 위치, 밸브 크기, 마찰, 강성, 요구 토크, 인지 오차, 발 디딤 조건 등의 다양한 변화를 평가할 수 있다. 주요 평가 지표에는 파지 성공률, 메커니즘 작업 완료율, 최대 상호작용력, 밸브 토크 생성 능력, 문 개방 시간, 재파지 횟수, 안정성 여유, 복구 성공률 등이 포함될 수 있다. 하드웨어 시험은 저하중 시험 장치에서 시작하여 실제 산업용 메커니즘과 제약된 작업 환경으로 단계적으로 확대하는 것이 적절하다.

문손잡이 및 밸브 조작은 4족 보행 로봇의 조작 시스템이 인지, 접촉 제어(Contact Control), 힘 추론(Force Reasoning), 이동을 통합해야 하는 이유를 명확하게 보여준다. 로봇 팔은 정밀한 상호작용을 제공하지만 성공적인 작업은 전체 로봇이 환경에서 발생하는 힘을 어떻게 지지하고 대응하는지에 의해 결정된다. 파지, 순응 제어(Compliant Control), 전신 안정화, 스테핑, 복구 기능을 협조함으로써 로봇 팔이 장착된 4족 보행 로봇은 복잡한 산업 환경에서 이동성을 유지하면서 사람이 사용하도록 설계된 다양한 기계 장치를 조작할 수 있다.

##  

## 09.06. Payload Delivery and Placement [w/Code]

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

Payload delivery and placement extends quadruped manipulation beyond object pickup by requiring the robot to transport a grasped load through changing terrain and place it accurately at a destination. The task couples locomotion, payload-aware dynamics, manipulation planning, perception, and contact control over an extended period. Unlike a short grasping action, the payload continuously modifies the robot's mass distribution, actuator loading, collision geometry, and balance conditions during travel.

A delivery task begins by characterizing the payload and the destination. Relevant payload properties include estimated mass, dimensions, center of mass, grasp configuration, fragility, and allowable orientation. The destination may impose placement position, orientation, clearance, insertion depth, or contact requirements. These properties determine whether the object should be carried close to the trunk, held at a specific attitude, or repositioned before the final placement phase.

After pickup, the object becomes part of the effective multibody system. Its mass changes the combined center of mass and modifies the inertia observed during acceleration, turning, and body rotation. An object held far from the trunk creates larger moments than the same object carried close to the body. Payload-aware control should therefore update the dynamic model or compensate for the additional load when calculating joint torques, contact forces, and feasible locomotion commands.

Payload estimation can be performed from known object information or inferred after lifting. Joint torque, force-torque sensing, gripper measurements, and arm configuration can provide observations from which mass and approximate center-of-mass location are estimated. The estimate need not be perfectly accurate to be useful. Even a bounded classification such as light, moderate, or heavy can allow the controller to select more conservative gait parameters and manipulation limits.

The carrying posture strongly affects stability and energy consumption. A compact arm configuration generally reduces the moment generated around the quadruped base and decreases collision exposure. However, some payloads require a particular orientation to prevent spilling, damage, or loss of grasp. The planner must therefore balance compactness, object constraints, camera visibility, arm manipulability, and the ability to react to terrain disturbances while selecting a transport configuration.

Whole-body control coordinates payload compensation with locomotion. As the robot walks, the controller regulates trunk attitude and center-of-mass behavior while distributing ground reaction forces among stance feet. The additional wrench created by the payload can be incorporated into the optimization. If the arm is offset to one side, the controller may shift the trunk, modify stance forces, or adjust footholds to counter the resulting roll moment and preserve sufficient stability margin.

Gait parameters should adapt to payload conditions rather than remaining identical to unloaded locomotion. A heavy or extended load may require lower velocity, reduced acceleration, shorter steps, longer stance duration, or smoother gait transitions. Sudden turns and rapid body rotations can create large inertial forces at the gripper. A payload-aware gait manager can therefore limit commanded motion according to estimated mass, arm extension, terrain difficulty, and available actuator capability.

Terrain perception becomes especially important because the consequences of a poor foothold increase when carrying a load. Slopes, steps, loose ground, and discrete obstacles can generate trunk disturbances that propagate into the manipulator and payload. The navigation system can prefer routes with greater traversability margin even when they are slightly longer. Route cost can incorporate payload stability, expected body motion, required clearance, and recovery opportunities in addition to geometric distance.

Collision geometry must be updated immediately after the object is acquired. A carried box, tool, container, or component may extend beyond the normal robot envelope and collide with walls, railings, vegetation, machinery, or the robot's own legs. Planning should represent the payload as an attached collision object whose pose changes with the arm. This is essential when passing through doorways, turning in confined spaces, or negotiating terrain that requires large body posture changes.

Grasp stability should be monitored throughout transport. Walking vibration, impact, arm motion, and changing gravity direction on slopes can cause gradual slip even when the initial grasp was secure. Tactile sensors, gripper position, motor current, force-torque measurements, or visual tracking can detect changes in grasp condition. The controller can increase grip force within safe limits, reduce locomotion intensity, reposition the arm, or stop before the payload is lost.

Fragile or orientation-sensitive payloads require motion-quality constraints beyond conventional robot stability. A container holding liquid may need limited tilt and acceleration, while delicate equipment may impose shock or vibration limits. The planner can constrain payload angular velocity, linear acceleration, jerk, or orientation relative to gravity. These limits should propagate into gait generation so that locomotion commands remain compatible with the physical requirements of the transported object.

Navigation and manipulation should remain coupled as the robot approaches the delivery location. The navigation system should not merely drive to a single point and then hand control to the arm. Instead, the final approach should consider manipulator reachability, destination visibility, terrain support, collision clearance, and required placement direction. A slightly different base pose can greatly improve placement accuracy and reduce the amount of arm extension required.

Destination perception refines the placement target during the final approach. Cameras or depth sensors can identify shelves, trays, fixtures, containers, tables, or designated placement regions and estimate their pose relative to the robot. When geometric tolerances are tight, wrist-mounted perception can provide local measurements after global navigation has positioned the quadruped nearby. Visual feedback can then compensate for localization error and uncertainty in the environment model.

Placement planning should distinguish between free placement and constrained placement. Placing an object on an open surface primarily requires collision-free motion and stable support after release. Inserting a component into a holder, slot, rack, or fixture imposes additional geometric constraints and may require precise orientation. The controller should select an approach direction that preserves visibility, avoids singular configurations, and provides sufficient compliance for the expected contact condition.

The transition from carrying to placement often requires changing the arm configuration significantly. The payload may be transported close to the trunk for stability but must be extended outward to reach the destination. This extension shifts the combined center of mass and increases joint torque just as precise positioning becomes important. Whole-body control can compensate by changing trunk position, lowering the body, widening support, or redistributing stance forces before the final placement motion.

Contact-aware placement is preferable when the destination surface position is uncertain. Rather than relying entirely on a predefined vertical coordinate, the robot can approach slowly and detect contact through force, torque, tactile, or gripper signals. Once support is detected, the controller can reduce downward force and allow the object to settle. Compliant behavior prevents excessive force from being transmitted into the object, supporting structure, manipulator, or quadruped body.

Precise placement may use visual servoing together with force control. Vision provides lateral and rotational alignment before contact, while force sensing becomes increasingly important after contact occurs. For constrained insertion, small compliant search motions can compensate for residual pose error. The system should distinguish successful seating from jamming by monitoring motion, contact wrench, and expected insertion progress rather than assuming that commanded displacement corresponds directly to object motion.

Release should occur only after the payload is confirmed to be supported by the destination. Premature gripper opening can drop the object, while delayed release may disturb an object that has already settled. Support can be inferred from changes in gripper load, arm force, object pose, or contact state. After opening the gripper, the robot should verify that the object remains stable before retracting the manipulator and resuming locomotion.

Arm retraction must also be planned because the placed object and surrounding structures remain collision hazards. The shortest reverse trajectory is not always safe, particularly after insertion or placement inside a confined region. A retreat path should preserve clearance while moving the arm toward a compact locomotion configuration. Once the manipulator is clear, the quadruped can restore its nominal posture and transition from manipulation mode back to normal navigation.

Delivery failures require explicit recovery logic. The robot may detect payload slip, excessive joint torque, blocked navigation, an unreachable placement target, unexpected contact, or unstable support after release. Recovery can include stopping locomotion, lowering the object to a safe surface, adjusting the grasp, selecting another base pose, replanning the route, or retrying placement. Protecting the robot and payload should take priority over completing the original trajectory.

Safety supervision should account for the combined robot-payload system. Joint torque, gripper force, stability margin, foot contact quality, arm extension, payload acceleration, and collision clearance can all define operational limits. When these limits are approached, the system can reduce speed or transition to a safer posture. A heavy payload should never be treated as an isolated arm load because its dynamic effects propagate through the trunk, legs, and ground contacts.

Simulation provides a practical environment for evaluating payload mass, center-of-mass offset, grasp location, gait speed, terrain, friction, route geometry, and placement tolerance. Performance metrics can include delivery success rate, payload retention, placement position and orientation error, peak joint torque, stability margin, transport time, energy consumption, and recovery frequency. Hardware validation can progress from light rigid objects to heavier and more fragile payloads.

Payload delivery and placement demonstrates the complete manipulation cycle of an arm-equipped quadruped: acquire an object, incorporate it into the robot's dynamic state, transport it through the environment, establish a manipulation-compatible destination pose, place it through controlled contact, verify release, and recover locomotion posture. Coordinating these stages transforms the quadruped from a mobile carrier into a terrain-capable autonomous material-handling system.

페이로드 운송 및 배치(Payload Delivery and Placement)는 4족 보행 로봇의 조작 능력을 단순한 객체 픽업(Object Pickup)에서 확장하여, 파지한 하중을 변화하는 지형을 통과해 운반하고 목적지에 정확하게 배치하도록 한다. 이 작업은 장시간에 걸쳐 이동(Locomotion), 페이로드 인식 동역학(Payload-Aware Dynamics), 조작 계획(Manipulation Planning), 인지(Perception), 접촉 제어(Contact Control)를 결합한다. 짧은 파지 동작과 달리 페이로드는 운송 과정 전체에서 로봇의 질량 분포, 액추에이터 부하, 충돌 형상, 균형 조건을 지속적으로 변화시킨다.

운송 작업은 페이로드와 목적지의 특성을 파악하는 것에서 시작한다. 중요한 페이로드 특성에는 추정 질량, 크기, 질량중심(Center of Mass), 파지 구성, 취약성, 허용 가능한 방향 등이 포함된다. 목적지에서는 배치 위치, 방향, 여유 공간, 삽입 깊이 또는 접촉 조건 등이 요구될 수 있다. 이러한 특성에 따라 객체를 몸통 가까이에서 운반할지, 특정 자세로 유지할지 또는 최종 배치 단계 전에 다시 위치를 조정할지가 결정된다.

픽업 이후 객체는 실질적인 다물체 시스템(Multibody System)의 일부가 된다. 객체 질량은 결합 질량중심(Combined Center of Mass)을 변화시키며 가속, 선회, 몸체 회전 과정에서 나타나는 관성 특성도 변화시킨다. 몸통에서 멀리 떨어진 위치에 객체를 들고 있으면 동일한 객체를 몸체 가까이에서 운반하는 경우보다 더 큰 모멘트가 발생한다. 따라서 페이로드 인식 제어(Payload-Aware Control)는 관절 토크, 접촉력, 실행 가능한 이동 명령을 계산할 때 동역학 모델을 갱신하거나 추가 하중을 보상해야 한다.

페이로드 추정(Payload Estimation)은 알려진 객체 정보를 이용하거나 객체를 들어 올린 이후 추론하여 수행할 수 있다. 관절 토크, 힘-토크 센싱(Force-Torque Sensing), 그리퍼 측정값, 로봇 팔 자세를 이용하여 질량과 대략적인 질량중심 위치를 추정할 수 있다. 이러한 추정값이 완벽하게 정확할 필요는 없다. 가벼움, 중간, 무거움과 같은 제한된 등급 분류만으로도 제어기가 더욱 보수적인 보행 파라미터와 조작 한계를 선택하는 데 유용하게 활용할 수 있다.

운반 자세(Carrying Posture)는 안정성과 에너지 소비에 큰 영향을 준다. 일반적으로 로봇 팔을 몸체 가까이 접은 자세는 4족 보행 로봇 베이스 주변에 발생하는 모멘트를 감소시키고 충돌 위험도 줄여준다. 그러나 일부 페이로드는 내용물의 유출, 손상 또는 파지 손실을 방지하기 위해 특정 방향을 유지해야 한다. 따라서 계획기는 운송 자세를 선택할 때 자세의 간결성, 객체 제약조건, 카메라 가시성, 로봇 팔 조작성(Manipulability), 지형 외란에 대응할 수 있는 능력을 함께 고려해야 한다.

전신 제어(Whole-Body Control)는 페이로드 보상과 이동을 협조한다. 로봇이 보행하는 동안 제어기는 몸통 자세와 질량중심 움직임을 조절하면서 지지 발 사이에 지면 반력(Ground Reaction Force)을 분배한다. 페이로드에 의해 발생하는 추가 렌치(Wrench)를 최적화 문제에 포함할 수 있다. 로봇 팔이 한쪽으로 치우쳐 있다면 제어기는 몸통을 이동시키거나 지지력을 변경하고 발 디딤 위치를 조정하여 발생하는 롤 모멘트(Roll Moment)를 상쇄하고 충분한 안정성 여유(Stability Margin)를 유지할 수 있다.

보행 파라미터(Gait Parameter)는 무부하 이동과 동일하게 유지하기보다 페이로드 조건에 따라 조정되어야 한다. 무겁거나 몸체에서 멀리 뻗은 하중은 낮은 속도, 작은 가속도, 짧은 보폭, 긴 지지 시간 또는 더욱 부드러운 보행 전환을 요구할 수 있다. 갑작스러운 선회와 빠른 몸체 회전은 그리퍼에 큰 관성력을 발생시킬 수 있다. 따라서 페이로드 인식 보행 관리자(Payload-Aware Gait Manager)는 추정 질량, 로봇 팔 확장 정도, 지형 난이도, 사용 가능한 액추에이터 성능에 따라 명령된 움직임을 제한할 수 있다.

하중을 운반하는 상황에서는 부적절한 발 디딤으로 인한 영향이 커지기 때문에 지형 인지(Terrain Perception)가 특히 중요하다. 경사면, 계단, 느슨한 지면, 독립적인 장애물은 몸통 외란을 발생시키고 이러한 외란이 매니퓰레이터와 페이로드로 전달될 수 있다. 내비게이션 시스템(Navigation System)은 경로가 약간 길어지더라도 더 높은 주행 가능성 여유(Traversability Margin)를 제공하는 경로를 선택할 수 있다. 경로 비용에는 기하학적 거리뿐만 아니라 페이로드 안정성, 예상 몸체 운동, 필요한 여유 공간, 복구 가능성 등을 포함할 수 있다.

객체를 획득한 직후 충돌 형상(Collision Geometry)을 갱신해야 한다. 운반 중인 상자, 도구, 용기 또는 부품은 일반적인 로봇 외곽보다 돌출되어 벽, 난간, 식생, 기계 설비 또는 로봇 자신의 다리와 충돌할 수 있다. 계획 시스템은 페이로드를 로봇 팔과 함께 자세가 변화하는 부착 충돌 객체(Attached Collision Object)로 표현해야 한다. 이는 출입구를 통과하거나 협소한 공간에서 회전하고 큰 몸체 자세 변화가 필요한 지형을 이동할 때 특히 중요하다.

파지 안정성(Grasp Stability)은 운송 과정 전체에서 지속적으로 감시해야 한다. 보행 진동, 충격, 로봇 팔 움직임, 경사면에서 변화하는 중력 방향은 초기 파지가 안정적이었더라도 점진적인 미끄러짐을 발생시킬 수 있다. 촉각 센서(Tactile Sensor), 그리퍼 위치, 모터 전류, 힘-토크 측정 또는 시각 추적을 통해 파지 상태 변화를 감지할 수 있다. 제어기는 안전 한계 내에서 파지력을 증가시키거나 이동 강도를 줄이고 로봇 팔 자세를 변경하거나 페이로드를 잃기 전에 정지할 수 있다.

깨지기 쉽거나 방향에 민감한 페이로드(Orientation-Sensitive Payload)는 일반적인 로봇 안정성을 넘어서는 운동 품질 제약조건(Motion-Quality Constraint)을 요구한다. 액체가 들어 있는 용기는 기울기와 가속도를 제한해야 할 수 있으며, 정밀 장비는 충격 또는 진동 한계를 요구할 수 있다. 계획기는 페이로드의 각속도, 선형 가속도, 저크(Jerk) 또는 중력 방향에 대한 자세를 제한할 수 있다. 이러한 한계는 보행 생성(Gait Generation) 단계까지 전달되어 이동 명령이 운반 객체의 물리적 요구조건과 일치하도록 해야 한다.

로봇이 운송 목적지에 접근할수록 내비게이션과 조작은 계속 결합된 상태로 유지되어야 한다. 내비게이션 시스템이 단순히 하나의 위치까지 이동한 후 제어권을 로봇 팔에 넘기는 방식으로 동작해서는 안 된다. 대신 최종 접근 과정에서 매니퓰레이터 도달 가능성, 목적지 가시성, 지형 지지 상태, 충돌 여유, 필요한 배치 방향을 고려해야 한다. 베이스 자세를 조금만 변경해도 배치 정확도를 크게 향상시키고 필요한 로봇 팔 확장 정도를 줄일 수 있다.

목적지 인지(Destination Perception)는 최종 접근 과정에서 배치 목표를 정밀하게 보정한다. 카메라 또는 깊이 센서를 이용하여 선반, 트레이, 고정구, 용기, 테이블 또는 지정된 배치 영역을 식별하고 로봇을 기준으로 해당 자세를 추정할 수 있다. 기하학적 허용오차가 작은 경우에는 전역 내비게이션으로 4족 보행 로봇을 주변에 위치시킨 후 손목 장착 인지(Wrist-Mounted Perception)를 이용하여 국부적인 측정값을 얻을 수 있다. 이후 시각 피드백을 이용하여 위치 추정 오차와 환경 모델의 불확실성을 보상할 수 있다.

배치 계획(Placement Planning)은 자유 배치(Free Placement)와 제약 배치(Constrained Placement)를 구분해야 한다. 열린 표면 위에 객체를 놓는 작업은 주로 충돌 없는 움직임과 해제 이후의 안정적인 지지를 요구한다. 반면 부품을 홀더, 슬롯, 랙 또는 고정구에 삽입하는 작업은 추가적인 기하학적 제약조건을 가지며 정밀한 방향 정렬이 필요할 수 있다. 제어기는 가시성을 유지하고 특이점 자세를 피하면서 예상되는 접촉 조건에 충분한 순응성(Compliance)을 제공하는 접근 방향을 선택해야 한다.

운반에서 배치로 전환하는 과정에서는 로봇 팔 자세를 크게 변경해야 하는 경우가 많다. 안정적인 운송을 위해 페이로드를 몸통 가까이에서 유지했더라도 목적지에 도달하려면 바깥쪽으로 로봇 팔을 뻗어야 할 수 있다. 이러한 확장은 정밀한 위치 결정이 필요한 순간에 결합 질량중심을 이동시키고 관절 토크를 증가시킨다. 전신 제어기는 최종 배치 동작 전에 몸통 위치를 변경하거나 몸체를 낮추고 지지 자세를 넓히거나 지지력을 재분배하여 이를 보상할 수 있다.

목적지 표면 위치에 불확실성이 존재하는 경우에는 접촉 인식 배치(Contact-Aware Placement)가 바람직하다. 사전에 정의된 수직 좌표에만 의존하기보다 로봇은 천천히 접근하면서 힘, 토크, 촉각 또는 그리퍼 신호를 이용하여 접촉을 감지할 수 있다. 지지가 확인되면 제어기는 아래쪽으로 가해지는 힘을 감소시키고 객체가 자연스럽게 안착하도록 할 수 있다. 순응 동작(Compliant Behavior)은 객체, 지지 구조물, 매니퓰레이터 또는 4족 보행 로봇 몸체에 과도한 힘이 전달되는 것을 방지한다.

정밀 배치(Precise Placement)에서는 시각 서보잉(Visual Servoing)과 힘 제어(Force Control)를 함께 사용할 수 있다. 접촉 전에는 비전을 이용하여 측면 및 회전 정렬을 수행하고, 접촉 이후에는 힘 센싱이 더욱 중요해진다. 제약된 삽입 작업에서는 작은 순응 탐색 동작(Compliant Search Motion)을 이용하여 남아 있는 자세 오차를 보상할 수 있다. 시스템은 명령된 변위가 실제 객체 이동과 동일하다고 가정하지 않고 움직임, 접촉 렌치, 예상 삽입 진행 상태를 감시하여 정상적인 안착과 걸림(Jamming)을 구분해야 한다.

페이로드가 목적지에 의해 안정적으로 지지되고 있다는 것이 확인된 이후에만 해제(Release)를 수행해야 한다. 그리퍼를 너무 일찍 열면 객체가 떨어질 수 있으며, 지나치게 늦게 해제하면 이미 안착된 객체를 다시 움직일 수 있다. 그리퍼 하중 변화, 로봇 팔에 작용하는 힘, 객체 자세 또는 접촉 상태를 이용하여 지지 여부를 추정할 수 있다. 그리퍼를 연 후에는 매니퓰레이터를 후퇴시키고 다시 이동을 시작하기 전에 객체가 안정적인 상태를 유지하고 있는지 확인해야 한다.

배치된 객체와 주변 구조물은 계속 충돌 위험 요소로 남아 있기 때문에 로봇 팔 후퇴(Arm Retraction) 역시 계획되어야 한다. 특히 협소한 영역 내부에 객체를 삽입하거나 배치한 경우에는 가장 짧은 역방향 궤적이 반드시 안전한 것은 아니다. 후퇴 경로(Retreat Path)는 충분한 충돌 여유를 유지하면서 로봇 팔을 이동에 적합한 간결한 자세로 복귀시켜야 한다. 매니퓰레이터가 주변 구조물에서 충분히 벗어나면 4족 보행 로봇은 정상 자세를 복원하고 조작 모드에서 일반 내비게이션 모드로 전환할 수 있다.

운송 실패에는 명시적인 복구 로직(Recovery Logic)이 필요하다. 로봇은 페이로드 미끄러짐, 과도한 관절 토크, 차단된 이동 경로, 도달 불가능한 배치 목표, 예상하지 못한 접촉 또는 해제 이후의 불안정한 지지를 감지할 수 있다. 복구 동작에는 이동 중지, 객체를 안전한 표면에 내려놓기, 파지 조정, 다른 베이스 자세 선택, 경로 재계획 또는 배치 재시도 등이 포함될 수 있다. 원래 계획된 궤적을 완료하는 것보다 로봇과 페이로드를 보호하는 것이 우선되어야 한다.

안전 감독(Safety Supervision)은 로봇과 페이로드가 결합된 전체 시스템을 고려해야 한다. 관절 토크, 그리퍼 힘, 안정성 여유, 발 접촉 품질, 로봇 팔 확장 정도, 페이로드 가속도, 충돌 여유 등이 모두 운용 한계를 정의할 수 있다. 이러한 한계에 접근하면 시스템은 속도를 줄이거나 보다 안전한 자세로 전환할 수 있다. 무거운 페이로드의 동역학적 영향은 몸통, 다리, 지면 접촉까지 전달되므로 단순히 로봇 팔에 가해지는 독립적인 하중으로 취급해서는 안 된다.

시뮬레이션(Simulation)은 페이로드 질량, 질량중심 오프셋, 파지 위치, 보행 속도, 지형, 마찰, 경로 형상, 배치 허용오차 등을 평가하기 위한 실용적인 환경을 제공한다. 성능 지표에는 운송 성공률, 페이로드 유지 성능, 배치 위치 및 방향 오차, 최대 관절 토크, 안정성 여유, 운송 시간, 에너지 소비, 복구 발생 빈도 등이 포함될 수 있다. 하드웨어 검증(Hardware Validation)은 가벼운 강체 객체에서 시작하여 점차 무겁고 깨지기 쉬운 페이로드로 확장할 수 있다.

페이로드 운송 및 배치(Payload Delivery and Placement)는 로봇 팔을 장착한 4족 보행 로봇의 완전한 조작 사이클(Manipulation Cycle)을 보여준다. 객체를 획득하고, 이를 로봇의 동역학 상태에 포함시키며, 환경을 통과하여 운송하고, 조작에 적합한 목적지 자세를 형성한 후, 제어된 접촉을 통해 객체를 배치하고, 해제를 확인한 뒤 다시 이동 자세를 복원한다. 이러한 단계들을 협조함으로써 4족 보행 로봇은 단순한 이동형 운반 장치를 넘어 복잡한 지형에서 자율적으로 작업할 수 있는 물류 및 자재 취급 시스템(Autonomous Material-Handling System)으로 확장될 수 있다.

##  

## 09.07. Quadruped Loco Manip RL Policy [w/Code]

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

Reinforcement learning provides a powerful framework for quadruped loco-manipulation because locomotion, balance, arm motion, and physical interaction can be optimized as a coupled behavior rather than as independently engineered controllers. A loco-manipulation policy receives information about the robot, environment, and manipulation objective and produces coordinated actions that allow the quadruped to move its body while simultaneously positioning or controlling the manipulator.

The central design problem is determining what the policy should observe and control. Observations may include base orientation and velocity, joint positions and velocities, foot contact states, manipulator configuration, end-effector pose, previous actions, terrain information, object pose, and task commands. Depending on the architecture, exteroceptive observations from depth cameras or height maps can also be encoded so that locomotion and manipulation adapt to surrounding geometry.

Policy actions can operate at several levels of abstraction. A low-level policy may directly generate joint position targets, torque commands, or residual corrections for both legs and arm. A hierarchical policy can instead output desired base velocity, body pose, foothold adjustments, and end-effector commands that are executed by conventional controllers. The appropriate action space depends on required control bandwidth, training complexity, hardware safety, and the amount of model-based structure retained in the system.

A unified policy can learn correlations that are difficult to encode manually. Extending the arm forward may automatically cause the learned behavior to shift the trunk backward, alter stance forces, or change step timing. Reaching sideways may produce a wider support configuration, while carrying a heavy object may naturally result in slower locomotion and a compact arm posture. These coordinated responses emerge when training objectives properly represent both manipulation performance and locomotion stability.

Reward design is therefore one of the most important elements of loco-manipulation learning. The reward can combine end-effector tracking, object pose error, commanded locomotion tracking, body stability, foot-placement quality, energy consumption, smoothness, and task completion. Penalties can discourage excessive joint torque, foot slip, collisions, unstable body orientation, abrupt actions, or joint-limit violations. Reward terms should be balanced so that the policy cannot improve manipulation performance by sacrificing basic locomotion safety.

Sparse task rewards may be insufficient for complex manipulation sequences because successful completion can be rare during early training. Curriculum learning can begin with simplified tasks such as stationary reaching, then introduce body repositioning, stepping, object contact, grasping, payload transport, and dynamic locomotion. Task difficulty can increase gradually through larger target ranges, rougher terrain, heavier payloads, stronger disturbances, and tighter placement tolerances as policy performance improves.

Hierarchical reinforcement learning can separate long-horizon task decisions from fast whole-body coordination. A high-level policy may select target object poses, manipulation phases, desired base locations, or locomotion commands, while a low-level policy generates dynamically consistent joint behavior. This decomposition reduces the burden on a single neural network and allows learned components to coexist with deterministic planners, state machines, whole-body controllers, and safety supervisors.

Residual reinforcement learning provides another practical architecture. Instead of replacing an existing locomotion or manipulation controller, the learned policy produces corrections to nominal commands. A model-based controller can preserve balance, contact constraints, and basic tracking, while reinforcement learning compensates for modeling error or improves task-specific coordination. Residual magnitude can be bounded so that the learned component cannot arbitrarily override the stable baseline controller.

Training generally relies on physics simulation because loco-manipulation requires very large numbers of interactions and failures during exploration. Parallel simulation can generate experience across many robot instances with different targets, terrain configurations, object properties, and disturbances. Efficient GPU-based simulation allows policies to experience a broader state distribution than would be practical on hardware, while avoiding mechanical wear and safety risks during early learning.

The simulator must represent both locomotion and manipulation contacts with sufficient fidelity. Foot-ground friction, actuator dynamics, arm inertia, gripper contact, payload mass, joint limits, latency, and collision behavior influence the learned strategy. An unrealistic model may produce behaviors that exploit simulation artifacts, such as excessive contact impulses or unrealistically fast actuator response. Training should therefore emphasize physically plausible dynamics rather than only maximizing simulated reward.

Domain randomization improves robustness by varying parameters that are uncertain in the real system. Robot mass, payload properties, motor strength, joint damping, friction, terrain geometry, sensor noise, communication delay, object pose, and external disturbances can be randomized between episodes. The objective is not to reproduce one physical robot perfectly but to train a policy that remains effective across a distribution containing the real operating conditions.

Privileged learning can further improve training efficiency. A teacher policy may receive simulator-only information such as exact terrain geometry, contact forces, object states, friction coefficients, or payload parameters. A student policy is then trained to reproduce useful behavior using only observations available on the physical robot. This approach allows rich simulation information to guide learning without requiring unavailable privileged variables during deployment.

Object interaction introduces discontinuous dynamics that make policy learning more difficult. The system transitions from free-space reaching to contact, grasping, lifting, carrying, and release, with different physical constraints in each phase. A policy can learn these transitions directly, but explicit phase information or hierarchical task structure may improve reliability. Contact sensors and force estimates are particularly valuable because visual information alone may not reveal whether a grasp or environmental contact is mechanically secure.

Dynamic loco-manipulation also requires temporal coordination. The policy may learn to synchronize arm acceleration with favorable gait phases, reduce reaching motion during vulnerable support transitions, or modify stepping when interaction forces increase. Recurrent neural networks, temporal observation histories, or state estimators can provide information about recent motion and contacts. Temporal context is useful when instantaneous observations cannot fully describe hidden dynamics or delayed actuator response.

Payload manipulation should be included explicitly during training because an acquired object changes the robot dynamics. Randomized payload mass and center-of-mass offset can teach the policy to adjust body posture, gait, and arm configuration automatically. Training can also include grasp uncertainty or slight object motion inside the gripper. A robust policy should maintain balance and task progress without requiring exact prior knowledge of every payload.

Safety constraints should not rely exclusively on learned rewards. A policy may encounter states outside the training distribution or exploit unintended reward tradeoffs. Deployment architectures should therefore retain deterministic limits on joint position, velocity, torque, collision, body attitude, contact force, and workspace boundaries. A safety layer can filter, clamp, or reject policy actions, while an independent supervisor can trigger stopping, arm retraction, or posture recovery.

Policy inference must satisfy real-time computational requirements on the onboard computer. Observation preprocessing, neural-network execution, action filtering, and communication should complete within the control period with bounded latency. Large perception encoders may run at lower frequency than proprioceptive control. A practical architecture can combine a fast policy for whole-body action generation with slower vision or task modules whose outputs are maintained between updates.

Sim-to-real transfer should be evaluated progressively rather than deploying a fully dynamic policy immediately. Initial hardware tests can use stationary reaching and low-force arm motion, followed by controlled stepping, payload handling, and simple contact tasks. Walking speed, terrain difficulty, interaction force, and manipulation range can then be increased gradually. Logged discrepancies between simulation and hardware can guide further system identification, randomization, and policy retraining.

Policy evaluation should measure more than accumulated reinforcement-learning reward. Relevant metrics include locomotion tracking error, end-effector accuracy, task success rate, grasp retention, payload stability, foot slip, energy use, peak torque, collision frequency, recovery success, and robustness to disturbances. Evaluation across unseen terrain, object poses, payloads, and friction conditions is necessary to determine whether the learned behavior generalizes beyond its training distribution.

Failure analysis is particularly important because learned policies may fail in ways that are difficult to predict from nominal trajectories. Tests should identify whether failures originate from perception error, insufficient exploration, reward imbalance, actuator saturation, contact-model mismatch, or out-of-distribution states. Recorded observations, actions, rewards, contact states, and safety interventions can be replayed to reproduce failures and construct targeted training scenarios for subsequent policy versions.

A production loco-manipulation system is therefore likely to be hybrid rather than purely learned. Reinforcement learning can provide adaptive whole-body coordination, while model-based control enforces dynamic structure, perception supplies environment state, planners manage long-horizon objectives, and safety logic constrains execution. The learned policy becomes one component within a larger robotics software stack rather than an unrestricted controller responsible for every system function.

Quadruped loco-manipulation reinforcement learning ultimately aims to create behaviors in which walking and manipulation emerge as one coordinated physical skill. The robot can reposition its body to improve reach, modify gait in response to arm motion, compensate for payloads, and adapt to contact forces without requiring every coupling to be manually programmed. When combined with robust simulation, domain randomization, hierarchical control, and explicit safety mechanisms, such policies provide a scalable path toward adaptive quadruped manipulation.

강화학습(Reinforcement Learning)은 이동, 균형, 로봇 팔 움직임, 물리적 상호작용을 서로 독립적으로 설계된 제어기가 아니라 하나의 결합된 행동으로 최적화할 수 있기 때문에 4족 보행 로봇의 로코-매니퓰레이션(Loco-Manipulation)에 강력한 프레임워크를 제공한다. 로코-매니퓰레이션 정책(Loco-Manipulation Policy)은 로봇, 환경, 조작 목표에 대한 정보를 입력받고, 4족 보행 로봇이 몸체를 이동시키면서 동시에 매니퓰레이터(Manipulator)의 위치나 동작을 제어할 수 있도록 협조된 행동을 생성한다.

핵심적인 설계 문제는 정책이 무엇을 관측하고 무엇을 제어해야 하는지를 결정하는 것이다. 관측값(Observation)에는 베이스 방향과 속도, 관절 위치와 속도, 발 접촉 상태, 매니퓰레이터 자세, 말단장치 자세(End-Effector Pose), 이전 행동, 지형 정보, 객체 자세, 작업 명령 등이 포함될 수 있다. 구조에 따라 깊이 카메라 또는 높이 맵(Height Map)에서 얻은 외부수용성 관측(Exteroceptive Observation)을 인코딩하여 이동과 조작이 주변 환경의 기하학적 구조에 적응하도록 만들 수도 있다.

정책 행동(Policy Action)은 여러 추상화 수준에서 동작할 수 있다. 저수준 정책(Low-Level Policy)은 다리와 로봇 팔 모두에 대해 관절 위치 목표, 토크 명령 또는 잔차 보정(Residual Correction)을 직접 생성할 수 있다. 계층형 정책(Hierarchical Policy)은 기존 제어기가 실행할 목표 베이스 속도, 몸체 자세, 발 디딤 보정, 말단장치 명령을 출력할 수 있다. 적절한 행동 공간(Action Space)은 요구되는 제어 대역폭, 학습 복잡도, 하드웨어 안전성, 시스템에 유지되는 모델 기반 구조의 정도에 따라 결정된다.

통합 정책(Unified Policy)은 수작업으로 명시하기 어려운 상관관계를 학습할 수 있다. 로봇 팔을 앞으로 뻗으면 학습된 행동이 자동으로 몸통을 뒤로 이동시키고, 지지력을 변경하거나 스텝 타이밍을 조정할 수 있다. 측면으로 리칭(Reaching)할 때에는 더 넓은 지지 자세가 나타날 수 있으며, 무거운 객체를 운반할 때에는 자연스럽게 이동 속도를 낮추고 로봇 팔을 몸체 가까이에 유지할 수 있다. 이러한 협조 행동은 학습 목표가 조작 성능과 이동 안정성을 적절하게 함께 표현할 때 나타난다.

따라서 보상 설계(Reward Design)는 로코-매니퓰레이션 학습에서 가장 중요한 요소 중 하나이다. 보상은 말단장치 추종, 객체 자세 오차, 명령된 이동 추종, 몸체 안정성, 발 디딤 품질, 에너지 소비, 움직임의 부드러움, 작업 완료 등을 결합할 수 있다. 과도한 관절 토크, 발 미끄러짐, 충돌, 불안정한 몸체 방향, 급격한 행동 또는 관절 한계 위반에는 페널티(Penalty)를 부여할 수 있다. 정책이 기본적인 이동 안전성을 희생하여 조작 성능만 향상시키지 못하도록 보상 항목 간 균형을 적절히 설정해야 한다.

복잡한 조작 순서에서는 초기 학습 단계에서 성공적인 작업 완료가 드물기 때문에 희소 작업 보상(Sparse Task Reward)만으로는 충분하지 않을 수 있다. 커리큘럼 학습(Curriculum Learning)은 정지 상태 리칭과 같은 단순한 작업에서 시작하여 몸체 재배치, 스테핑, 객체 접촉, 파지, 페이로드 운송, 동적 이동을 점진적으로 추가할 수 있다. 정책 성능이 향상됨에 따라 더 넓은 목표 범위, 거친 지형, 무거운 페이로드, 강한 외란, 엄격한 배치 허용오차 등을 적용하여 작업 난이도를 단계적으로 증가시킬 수 있다.

계층형 강화학습(Hierarchical Reinforcement Learning)은 장시간에 걸친 작업 의사결정과 빠른 전신 협조(Whole-Body Coordination)를 분리할 수 있다. 상위 정책(High-Level Policy)은 목표 객체 자세, 조작 단계, 원하는 베이스 위치 또는 이동 명령을 선택하고, 하위 정책(Low-Level Policy)은 동역학적으로 일관된 관절 행동을 생성할 수 있다. 이러한 분해는 하나의 신경망(Neural Network)에 가해지는 부담을 줄이고 학습 기반 구성요소가 결정론적 계획기, 상태 머신(State Machine), 전신 제어기, 안전 감독기와 함께 동작할 수 있도록 한다.

잔차 강화학습(Residual Reinforcement Learning)은 또 다른 실용적인 구조를 제공한다. 기존의 이동 또는 조작 제어기를 완전히 대체하는 대신 학습된 정책이 기준 명령에 대한 보정값을 생성한다. 모델 기반 제어기(Model-Based Controller)는 균형, 접촉 제약조건, 기본적인 추종 성능을 유지하고 강화학습은 모델링 오차를 보상하거나 작업별 협조 성능을 개선할 수 있다. 잔차 크기를 제한하면 학습 구성요소가 안정적인 기준 제어기를 임의로 무력화하는 것을 방지할 수 있다.

로코-매니퓰레이션 학습에는 탐색 과정에서 매우 많은 상호작용과 실패가 필요하기 때문에 일반적으로 물리 시뮬레이션(Physics Simulation)을 활용한다. 병렬 시뮬레이션(Parallel Simulation)은 서로 다른 목표, 지형 구성, 객체 특성, 외란을 가진 다수의 로봇 인스턴스에서 경험을 생성할 수 있다. 효율적인 GPU 기반 시뮬레이션(GPU-Based Simulation)을 사용하면 실제 하드웨어에서 구현하기 어려울 정도로 넓은 상태 분포를 경험하게 하면서 초기 학습 과정에서 발생하는 기계적 마모와 안전 위험을 방지할 수 있다.

시뮬레이터는 이동 접촉과 조작 접촉을 모두 충분한 충실도(Fidelity)로 표현해야 한다. 발-지면 마찰, 액추에이터 동역학, 로봇 팔 관성, 그리퍼 접촉, 페이로드 질량, 관절 한계, 지연 시간, 충돌 동작 등이 학습된 전략에 영향을 준다. 비현실적인 모델은 과도한 접촉 충격이나 비현실적으로 빠른 액추에이터 응답과 같은 시뮬레이션 인공 요소를 정책이 악용하도록 만들 수 있다. 따라서 학습에서는 단순히 시뮬레이션 보상을 최대화하는 것보다 물리적으로 타당한 동역학을 유지하는 것이 중요하다.

도메인 랜덤화(Domain Randomization)는 실제 시스템에서 불확실한 파라미터를 변화시켜 강건성(Robustness)을 향상시킨다. 로봇 질량, 페이로드 특성, 모터 출력, 관절 감쇠, 마찰, 지형 형상, 센서 잡음, 통신 지연, 객체 자세, 외부 외란 등을 에피소드(Episode)마다 무작위로 변화시킬 수 있다. 목적은 하나의 실제 로봇을 완벽하게 재현하는 것이 아니라 실제 운용 조건을 포함하는 넓은 분포에서 효과적으로 동작하는 정책을 학습하는 것이다.

특권 학습(Privileged Learning)은 학습 효율을 더욱 향상시킬 수 있다. 교사 정책(Teacher Policy)은 정확한 지형 형상, 접촉력, 객체 상태, 마찰계수, 페이로드 파라미터와 같이 시뮬레이터에서만 얻을 수 있는 정보를 입력받을 수 있다. 이후 학생 정책(Student Policy)은 실제 로봇에서 사용 가능한 관측값만을 이용하여 유용한 행동을 재현하도록 학습된다. 이를 통해 실제 배치 단계에서 사용할 수 없는 특권 변수(Privileged Variable)를 요구하지 않으면서 풍부한 시뮬레이션 정보를 학습에 활용할 수 있다.

객체 상호작용(Object Interaction)은 불연속적인 동역학 변화를 발생시키기 때문에 정책 학습을 더욱 어렵게 만든다. 시스템은 자유공간 리칭에서 접촉, 파지, 인양, 운반, 해제로 전환되며 각 단계마다 서로 다른 물리적 제약조건이 적용된다. 정책이 이러한 전환을 직접 학습할 수도 있지만, 명시적인 단계 정보나 계층형 작업 구조를 제공하면 신뢰성을 향상시킬 수 있다. 시각 정보만으로는 파지 또는 환경 접촉이 기계적으로 안정적인지 확인하기 어려울 수 있으므로 접촉 센서와 힘 추정값이 특히 중요하다.

동적 로코-매니퓰레이션(Dynamic Loco-Manipulation)은 시간적 협조(Temporal Coordination)도 필요로 한다. 정책은 유리한 보행 위상(Gait Phase)에 로봇 팔 가속을 동기화하고, 취약한 지지 전환 과정에서는 리칭 움직임을 줄이며, 상호작용력이 증가할 때 스테핑을 변경하도록 학습할 수 있다. 순환 신경망(Recurrent Neural Network), 시간적 관측 이력(Temporal Observation History), 상태 추정기(State Estimator)를 이용하여 최근 움직임과 접촉에 대한 정보를 제공할 수 있다. 순간적인 관측값만으로 숨겨진 동역학이나 지연된 액추에이터 응답을 완전히 설명할 수 없는 경우 시간적 문맥(Temporal Context)이 유용하다.

객체를 획득하면 로봇의 동역학이 변화하므로 페이로드 조작(Payload Manipulation)을 학습 과정에 명시적으로 포함해야 한다. 페이로드 질량과 질량중심 오프셋(Center-of-Mass Offset)을 무작위화하면 정책이 몸체 자세, 보행, 로봇 팔 구성을 자동으로 조정하도록 학습할 수 있다. 파지 불확실성이나 그리퍼 내부에서 발생하는 작은 객체 움직임도 학습에 포함할 수 있다. 강건한 정책은 모든 페이로드에 대한 정확한 사전 정보 없이도 균형과 작업 진행 상태를 유지해야 한다.

안전 제약조건(Safety Constraint)을 학습된 보상에만 의존해서는 안 된다. 정책은 학습 분포를 벗어난 상태를 경험하거나 의도하지 않은 보상 간 절충 관계를 악용할 수 있다. 따라서 실제 배치 구조에서는 관절 위치, 속도, 토크, 충돌, 몸체 자세, 접촉력, 작업공간 경계에 대한 결정론적 제한(Deterministic Limit)을 유지해야 한다. 안전 계층(Safety Layer)은 정책 행동을 필터링하거나 제한 또는 거부할 수 있으며, 독립적인 감독기는 정지, 로봇 팔 후퇴 또는 자세 복구를 실행할 수 있다.

정책 추론(Policy Inference)은 온보드 컴퓨터(Onboard Computer)의 실시간 계산 요구조건을 만족해야 한다. 관측 전처리, 신경망 실행, 행동 필터링, 통신 과정은 제한된 지연 시간 내에서 제어 주기(Control Period)를 만족하도록 완료되어야 한다. 대규모 인지 인코더(Perception Encoder)는 고유수용성 제어(Proprioceptive Control)보다 낮은 주파수에서 실행될 수 있다. 실용적인 구조에서는 전신 행동을 빠르게 생성하는 정책과 상대적으로 느리게 실행되면서 갱신 사이에 출력을 유지하는 비전 또는 작업 모듈을 결합할 수 있다.

시뮬레이션-실환경 전이(Sim-to-Real Transfer)는 완전한 동적 정책을 즉시 적용하기보다 단계적으로 평가해야 한다. 초기 하드웨어 시험에서는 정지 상태 리칭과 저하중 로봇 팔 움직임을 수행하고, 이후 제어된 스테핑, 페이로드 처리, 단순한 접촉 작업으로 확장할 수 있다. 이후 보행 속도, 지형 난이도, 상호작용력, 조작 범위를 점진적으로 증가시킬 수 있다. 시뮬레이션과 실제 하드웨어 사이에서 기록된 차이는 추가적인 시스템 식별(System Identification), 랜덤화, 정책 재학습에 활용할 수 있다.

정책 평가는 누적 강화학습 보상(Accumulated Reinforcement-Learning Reward)만을 측정해서는 안 된다. 관련 지표에는 이동 추종 오차, 말단장치 정확도, 작업 성공률, 파지 유지 성능, 페이로드 안정성, 발 미끄러짐, 에너지 사용량, 최대 토크, 충돌 빈도, 복구 성공률, 외란에 대한 강건성 등이 포함된다. 학습되지 않은 지형, 객체 자세, 페이로드, 마찰 조건에서 평가하여 학습된 행동이 학습 분포를 넘어 일반화(Generalization)되는지를 확인해야 한다.

학습된 정책은 정상 궤적만으로 예측하기 어려운 방식으로 실패할 수 있기 때문에 실패 분석(Failure Analysis)이 특히 중요하다. 시험을 통해 실패 원인이 인지 오차, 불충분한 탐색, 보상 불균형, 액추에이터 포화, 접촉 모델 불일치 또는 분포 외 상태(Out-of-Distribution State)에서 발생하는지 식별해야 한다. 기록된 관측값, 행동, 보상, 접촉 상태, 안전 개입 정보를 재생하여 실패를 재현하고 이후 정책 버전을 위한 표적 학습 시나리오를 구성할 수 있다.

따라서 실제 운용을 위한 로코-매니퓰레이션 시스템은 완전한 학습 기반 구조보다는 하이브리드 시스템(Hybrid System)이 될 가능성이 높다. 강화학습은 적응형 전신 협조를 제공하고, 모델 기반 제어(Model-Based Control)는 동역학적 구조를 강제하며, 인지 시스템은 환경 상태를 제공하고, 계획기는 장기적인 작업 목표를 관리하며, 안전 로직은 실행 범위를 제한할 수 있다. 학습된 정책은 모든 시스템 기능을 제한 없이 담당하는 제어기가 아니라 더 큰 로보틱스 소프트웨어 스택(Robotics Software Stack)을 구성하는 하나의 핵심 요소가 된다.

4족 보행 로봇의 로코-매니퓰레이션 강화학습(Quadruped Loco-Manipulation Reinforcement Learning)은 궁극적으로 보행과 조작이 하나의 협조된 물리적 기술로 나타나는 행동을 구현하는 것을 목표로 한다. 로봇은 도달 범위를 개선하기 위해 몸체 위치를 변경하고, 로봇 팔 움직임에 따라 보행 패턴을 수정하며, 페이로드를 보상하고, 모든 결합 관계를 사람이 직접 프로그래밍하지 않아도 접촉력에 적응할 수 있다. 강건한 시뮬레이션, 도메인 랜덤화, 계층형 제어, 명시적인 안전 메커니즘을 결합하면 이러한 정책은 적응형 4족 보행 로봇 조작(Adaptive Quadruped Manipulation)을 구현하기 위한 확장 가능한 경로를 제공한다.

##  

## 09.08. Manipulation During Dynamic Locomotion [w/Code]

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

Manipulation during dynamic locomotion requires a quadruped to perform purposeful arm motion while its base continuously translates, rotates, and oscillates under changing foot contacts. Unlike stationary manipulation, the reference frame supporting the arm is never truly fixed. The control system must therefore preserve manipulation accuracy while simultaneously managing gait dynamics, balance, terrain interaction, and disturbances generated by the manipulator itself.

The fundamental difficulty arises from dynamic coupling between the arm, trunk, and legs. Accelerating the manipulator changes the robot's total linear and angular momentum, while each foot touchdown produces forces that propagate through the floating base into the arm. A rapid reaching motion can disturb body attitude, and an aggressive step can disturb end-effector tracking. Dynamic manipulation must account for these interactions rather than treating locomotion as an independent disturbance source.

A useful representation models the robot as one floating-base multibody system containing leg and manipulator joints. Generalized coordinates describe base pose and joint configuration, while generalized velocities represent base and joint motion. Whole-body dynamics then relate accelerations, actuator torques, gravity, contact forces, and external manipulation wrenches. This unified representation allows the controller to reason explicitly about how arm commands influence locomotion and how gait motion influences manipulation.

End-effector objectives should normally be expressed in a task-relevant reference frame. A hand carrying an object may need to maintain a nearly constant world-frame orientation even while the trunk pitches and rolls over terrain. For interaction with a moving target, the command may instead be object-relative. Accurate coordinate transformations and state estimation are essential because base motion must be removed from or incorporated into the desired end-effector trajectory at every control update.

Gait phase strongly influences the manipulation capability available at a particular instant. During a stable multi-foot support phase, larger arm accelerations or interaction forces may be feasible. During contact transition or reduced support, the same command can produce excessive body motion or contact-force demand. A dynamic manipulation controller can therefore schedule arm motion according to gait phase, shifting demanding portions of a task toward intervals with greater support authority.

The manipulator can also assist locomotion by managing whole-body momentum. Arm motion does not always need to be treated as a disturbance that must be rejected. Properly coordinated arm acceleration can counter trunk rotation, reduce angular momentum, or help stabilize the body during aggressive maneuvers. This principle resembles natural arm swinging in human locomotion, but an articulated quadruped manipulator can intentionally generate task-compatible momentum while still progressing toward a manipulation objective.

Whole-body control provides a systematic framework for coordinating these behaviors. The controller can simultaneously track end-effector motion, regulate trunk orientation, control center-of-mass behavior, maintain stance-foot constraints, execute swing-leg trajectories, and respect actuator limits. Optimization-based formulations distribute required motion and force across the complete robot so that manipulation tracking is achieved without violating the physical requirements of dynamic locomotion.

Task priorities may need to vary according to operating conditions. Under nominal walking, end-effector accuracy can receive substantial control authority. If a foot slips or the robot encounters an unexpected terrain disturbance, balance recovery should temporarily dominate manipulation tracking. The arm trajectory can be slowed, softened, or suspended while the legs restore a viable support state. Once stability returns, manipulation can resume without requiring complete task cancellation.

Contact-force feasibility becomes especially important when the manipulator applies force to the environment during locomotion. An external wrench at the hand must ultimately be balanced through the robot and its ground contacts. As feet enter and leave stance, the available set of supporting forces changes. The controller should verify that required ground reaction forces remain within friction and actuator limits before commanding substantial pushing, pulling, or other contact-rich manipulation.

Model predictive control can anticipate future gait and manipulation interactions rather than reacting only to current errors. Over a finite prediction horizon, the controller can consider expected foot contacts, base motion, arm trajectory, interaction forces, and dynamic constraints. It may adjust future footholds or body motion to create a more favorable manipulation configuration. Predictive coordination is particularly valuable when an upcoming grasp, push, or placement event requires increased stability.

Trajectory generation should limit unnecessary acceleration and jerk because rapid manipulator motion can destabilize locomotion. Smooth end-effector trajectories reduce reaction forces transmitted to the trunk and improve tracking under finite actuator bandwidth. However, overly conservative motion can reduce task performance. Dynamic trajectory scaling can adjust arm speed according to gait phase, terrain condition, payload, stability margin, and current actuator utilization.

Payloads increase the coupling between manipulation and locomotion. Once an object is grasped, its mass and inertia become part of the effective robot dynamics. A payload held far from the trunk can significantly increase pitch or roll moments during acceleration. The controller should incorporate estimated payload properties and may move the arm toward a compact configuration during difficult terrain traversal while allowing greater extension when support conditions improve.

Perception must remain reliable despite body vibration and changing camera viewpoints. Cameras mounted on the trunk, head, or manipulator experience motion generated by gait and terrain impact. Accurate timestamping, inertial compensation, and state estimation are required to transform observations into stable world or object coordinates. Visual tracking can provide continuous target updates, while prediction compensates for perception latency during rapid robot and end-effector motion.

Visual servoing can correct manipulation errors caused by imperfect localization or dynamic base motion. Instead of relying entirely on a precomputed arm trajectory, image or pose feedback continuously updates the relative target error. The controller can then coordinate the arm and body to maintain alignment. Filtering must balance noise suppression against delay because excessive filtering can make the visual correction too slow for dynamic locomotion.

Terrain-aware manipulation should account for predicted body disturbances before they occur. Stepping onto a slope, obstacle, compliant surface, or height transition changes trunk motion and contact forces. If terrain perception predicts a difficult step, the system can temporarily retract the arm, reduce manipulation speed, or delay a precision interaction until a more stable gait phase. Manipulation planning therefore benefits directly from the same terrain model used for locomotion.

Self-collision constraints become more challenging during dynamic movement because the relative geometry of the arm, trunk, and legs changes rapidly. A manipulator configuration that is safe during stance may conflict with a swinging leg or become unsafe after body pitching. Online collision monitoring should consider predicted leg trajectories as well as current geometry. Maintaining preferred arm regions can reduce the probability of sudden avoidance motions during locomotion.

Dynamic manipulation also requires explicit management of actuator capacity. Leg actuators may approach torque limits while climbing or accelerating, leaving less whole-body authority for compensating arm disturbances. Similarly, arm joints carrying a payload may have limited ability to reject base motion. Monitoring torque, velocity, thermal state, and power utilization allows the controller to reduce manipulation intensity before combined locomotion and arm demands exceed hardware capability.

Recovery behavior should preserve both robot stability and manipulation safety. When balance deteriorates, the system may retract the arm, move a payload toward the trunk, reduce interaction force, or release a noncritical object if necessary. For contact tasks, uncontrolled arm withdrawal may itself create hazards, so recovery must consider environmental constraints. A task supervisor should select recovery actions according to current grasp, contact, terrain, and support conditions.

Learning-based control can complement model-based dynamic coordination. Reinforcement learning policies can discover timing relationships between gait and arm motion that are difficult to design manually, while residual policies can compensate for model errors. Training with randomized terrain, payloads, contact conditions, latency, and disturbances can improve robustness. Deterministic safety constraints should remain active so that learned actions cannot violate critical joint, collision, or stability limits.

Real-time implementation requires multiple control rates. Whole-body stabilization and joint control typically operate at high frequency, while trajectory planning, perception, terrain analysis, and task decisions can update more slowly. Shared timestamps and consistent robot-state estimates are essential across these layers. Delayed arm or target information can become especially damaging during dynamic locomotion because the base configuration may change significantly within a short interval.

Simulation should test combinations of walking speed, gait type, arm trajectory, payload, terrain, external force, and perception uncertainty. Useful metrics include end-effector tracking error, body attitude deviation, foot slip, contact-force margin, joint torque, manipulation success, gait disturbance, and recovery performance. Evaluation should compare stationary manipulation with progressively faster locomotion to identify where dynamic coupling begins to limit task accuracy or stability.

Hardware validation should progress from simple arm motion during slow walking toward more demanding coordinated tasks. Initial experiments can maintain a fixed world-frame hand pose while the quadruped walks, followed by reaching, carrying, grasping, and contact interaction. Terrain complexity and locomotion speed can then increase gradually. High-rate logging of state, contact, torque, trajectory, and perception data is necessary to identify coupling effects that are difficult to reproduce visually.

Manipulation during dynamic locomotion ultimately requires locomotion and arm control to function as one physical behavior. The legs create changing support, the trunk provides a moving manipulation base, and the arm introduces both task motion and dynamic reaction forces. By coordinating momentum, contact forces, gait phase, perception, and whole-body motion, the quadruped can perform useful manipulation without requiring locomotion to stop whenever precise interaction is needed.

동적 이동 중 조작(Manipulation During Dynamic Locomotion)은 4족 보행 로봇의 베이스가 변화하는 발 접촉 조건에서 지속적으로 병진, 회전, 진동하는 동안 목적을 가진 로봇 팔 움직임을 수행하도록 요구한다. 정지 상태 조작(Stationary Manipulation)과 달리 로봇 팔을 지지하는 기준 좌표계는 완전히 고정되어 있지 않다. 따라서 제어 시스템은 보행 동역학, 균형, 지형 상호작용, 매니퓰레이터 자체에서 발생하는 외란을 동시에 관리하면서 조작 정확도를 유지해야 한다.

근본적인 어려움은 로봇 팔, 몸통, 다리 사이의 동역학적 결합(Dynamic Coupling)에서 발생한다. 매니퓰레이터를 가속하면 로봇 전체의 선운동량과 각운동량이 변화하고, 각각의 발 착지(Foot Touchdown)는 부유 베이스(Floating Base)를 통해 로봇 팔로 전달되는 힘을 발생시킨다. 빠른 리칭(Reaching)은 몸체 자세를 교란할 수 있고 공격적인 스텝은 말단장치 추종을 방해할 수 있다. 동적 조작에서는 이동을 독립적인 외란 발생원으로 취급하지 않고 이러한 상호작용을 함께 고려해야 한다.

유용한 표현 방법은 로봇을 다리와 매니퓰레이터 관절을 포함하는 하나의 부유 베이스 다물체 시스템(Floating-Base Multibody System)으로 모델링하는 것이다. 일반화 좌표(Generalized Coordinate)는 베이스 자세와 관절 구성을 표현하고, 일반화 속도(Generalized Velocity)는 베이스 및 관절 움직임을 나타낸다. 이후 전신 동역학(Whole-Body Dynamics)은 가속도, 액추에이터 토크, 중력, 접촉력, 외부 조작 렌치(External Manipulation Wrench)의 관계를 정의한다. 이러한 통합 표현을 통해 로봇 팔 명령이 이동에 미치는 영향과 보행 움직임이 조작에 미치는 영향을 명시적으로 고려할 수 있다.

말단장치 목표(End-Effector Objective)는 일반적으로 작업과 관련된 기준 좌표계에서 표현해야 한다. 객체를 운반하는 손은 몸통이 지형을 따라 피치(Pitch)와 롤(Roll) 운동을 하더라도 월드 좌표계(World Frame)를 기준으로 거의 일정한 방향을 유지해야 할 수 있다. 움직이는 목표물과 상호작용하는 경우에는 객체 상대 좌표계(Object-Relative Frame)를 사용할 수 있다. 매 제어 갱신 시 베이스 움직임을 원하는 말단장치 궤적에서 제거하거나 적절하게 반영해야 하므로 정확한 좌표 변환과 상태 추정(State Estimation)이 필수적이다.

보행 위상(Gait Phase)은 특정 순간에 사용할 수 있는 조작 능력에 큰 영향을 미친다. 여러 발이 안정적으로 지지하는 구간에서는 더 큰 로봇 팔 가속도나 상호작용력을 허용할 수 있다. 반면 접촉 전환(Contact Transition) 또는 지지점이 감소하는 구간에서는 동일한 명령이 과도한 몸체 움직임이나 접촉력 요구를 발생시킬 수 있다. 따라서 동적 조작 제어기는 보행 위상에 따라 로봇 팔 움직임을 조정하여 높은 힘이 요구되는 작업 구간을 더 큰 지지 능력을 확보할 수 있는 시점으로 이동시킬 수 있다.

매니퓰레이터는 전신 운동량(Whole-Body Momentum)을 관리함으로써 이동 자체를 보조할 수도 있다. 로봇 팔 움직임을 항상 제거해야 하는 외란으로 취급할 필요는 없다. 적절하게 협조된 로봇 팔 가속은 몸통 회전을 상쇄하고 각운동량을 감소시키거나 공격적인 동작 중 몸체 안정화를 지원할 수 있다. 이러한 원리는 사람의 보행에서 자연스럽게 나타나는 팔 흔들기와 유사하지만, 관절형 매니퓰레이터를 가진 4족 보행 로봇은 조작 목표를 수행하면서 작업과 양립할 수 있는 운동량을 의도적으로 생성할 수 있다.

전신 제어(Whole-Body Control)는 이러한 행동을 협조하기 위한 체계적인 프레임워크를 제공한다. 제어기는 말단장치 움직임 추종, 몸통 방향 조절, 질량중심 동작 제어, 지지 발 제약조건 유지, 스윙 다리 궤적 실행, 액추에이터 한계 준수를 동시에 수행할 수 있다. 최적화 기반 구조(Optimization-Based Formulation)는 필요한 움직임과 힘을 로봇 전체에 분배하여 동적 이동에 필요한 물리적 요구조건을 위반하지 않으면서 조작 추종 성능을 확보한다.

작업 우선순위(Task Priority)는 운용 조건에 따라 변화해야 할 수 있다. 정상적인 보행에서는 말단장치 정확도에 상당한 제어 권한을 할당할 수 있다. 그러나 발이 미끄러지거나 로봇이 예상하지 못한 지형 외란을 만나면 균형 복구(Balance Recovery)가 일시적으로 조작 추종보다 높은 우선순위를 가져야 한다. 다리가 안정적인 지지 상태를 복구하는 동안 로봇 팔 궤적을 감속하거나 순응적으로 변경하거나 일시 중지할 수 있다. 안정성이 회복되면 전체 작업을 취소하지 않고 조작을 다시 시작할 수 있다.

매니퓰레이터가 이동 중 환경에 힘을 가하는 경우에는 접촉력 실행 가능성(Contact-Force Feasibility)이 특히 중요해진다. 손에 작용하는 외부 렌치는 궁극적으로 로봇 몸체와 지면 접촉을 통해 균형을 이루어야 한다. 발이 지지 상태에 진입하거나 이탈하면서 사용할 수 있는 지지력의 집합이 변화한다. 따라서 상당한 크기의 밀기, 당기기 또는 기타 접촉 중심 조작(Contact-Rich Manipulation)을 명령하기 전에 필요한 지면 반력(Ground Reaction Force)이 마찰 및 액추에이터 한계 내에서 유지되는지 확인해야 한다.

모델 예측 제어(Model Predictive Control)는 현재 오차에만 반응하는 대신 미래의 보행과 조작 사이의 상호작용을 예측할 수 있다. 제한된 예측 구간(Prediction Horizon)에서 예상되는 발 접촉, 베이스 움직임, 로봇 팔 궤적, 상호작용력, 동역학적 제약조건을 함께 고려할 수 있다. 제어기는 더욱 유리한 조작 자세를 만들기 위해 미래의 발 디딤 위치나 몸체 움직임을 조정할 수도 있다. 이러한 예측 협조(Predictive Coordination)는 향후 파지, 밀기 또는 배치 작업에서 높은 안정성이 요구되는 경우 특히 유용하다.

빠른 매니퓰레이터 움직임은 이동 안정성을 저하시킬 수 있으므로 궤적 생성(Trajectory Generation)에서는 불필요한 가속도와 저크(Jerk)를 제한해야 한다. 부드러운 말단장치 궤적은 몸통으로 전달되는 반력을 감소시키고 제한된 액추에이터 대역폭에서도 추종 성능을 향상시킨다. 그러나 지나치게 보수적인 움직임은 작업 성능을 저하시킬 수 있다. 동적 궤적 스케일링(Dynamic Trajectory Scaling)을 이용하면 보행 위상, 지형 조건, 페이로드, 안정성 여유, 현재 액추에이터 사용률에 따라 로봇 팔 속도를 조절할 수 있다.

페이로드(Payload)는 조작과 이동 사이의 결합을 더욱 증가시킨다. 객체를 파지하면 해당 객체의 질량과 관성이 실질적인 로봇 동역학의 일부가 된다. 몸통에서 멀리 떨어진 위치에 페이로드를 유지하면 가속 과정에서 피치 또는 롤 모멘트가 크게 증가할 수 있다. 제어기는 추정된 페이로드 특성을 동역학에 반영해야 하며, 어려운 지형을 이동할 때에는 로봇 팔을 몸체 가까이에 배치하고 지지 조건이 개선되면 더 큰 확장을 허용할 수 있다.

보행에 따른 몸체 진동과 지속적으로 변화하는 카메라 시점에도 인지(Perception)는 신뢰성을 유지해야 한다. 몸통, 헤드 또는 매니퓰레이터에 장착된 카메라는 보행과 지형 충격에 의해 발생하는 움직임을 경험한다. 관측값을 안정적인 월드 또는 객체 좌표계로 변환하려면 정확한 타임스탬프(Timestamp), 관성 보상(Inertial Compensation), 상태 추정이 필요하다. 시각 추적(Visual Tracking)은 지속적인 목표 갱신 정보를 제공하고, 예측 기법은 빠른 로봇 및 말단장치 움직임에서 발생하는 인지 지연을 보상할 수 있다.

시각 서보잉(Visual Servoing)은 불완전한 위치 추정이나 동적인 베이스 움직임으로 인해 발생하는 조작 오차를 보정할 수 있다. 사전에 계산된 로봇 팔 궤적에만 의존하는 대신 영상 또는 자세 피드백을 이용하여 상대적인 목표 오차를 지속적으로 갱신할 수 있다. 이후 제어기는 로봇 팔과 몸체를 협조하여 정렬 상태를 유지한다. 과도한 필터링은 동적 이동에 필요한 시각 보정 속도를 저하시킬 수 있으므로 필터링 과정에서는 잡음 억제와 지연 사이의 균형을 유지해야 한다.

지형 인식 조작(Terrain-Aware Manipulation)은 실제 외란이 발생하기 전에 예상되는 몸체 교란을 고려해야 한다. 경사면, 장애물, 순응성 표면 또는 높이 변화 구간을 밟으면 몸통 움직임과 접촉력이 변화한다. 지형 인지를 통해 어려운 스텝이 예상되면 시스템은 로봇 팔을 일시적으로 몸체 쪽으로 당기고, 조작 속도를 감소시키거나 정밀 상호작용을 더욱 안정적인 보행 위상까지 지연시킬 수 있다. 따라서 조작 계획은 이동에 사용되는 동일한 지형 모델(Terrain Model)을 직접 활용함으로써 성능을 향상시킬 수 있다.

동적 이동 중에는 로봇 팔, 몸통, 다리 사이의 상대적인 형상이 빠르게 변화하므로 자기 충돌 제약조건(Self-Collision Constraint)을 관리하기가 더욱 어려워진다. 지지 상태에서는 안전한 매니퓰레이터 자세가 스윙 중인 다리와 충돌하거나 몸체의 피치 변화 이후 위험한 상태가 될 수 있다. 온라인 충돌 감시(Online Collision Monitoring)는 현재 형상뿐만 아니라 예측된 다리 궤적까지 고려해야 한다. 로봇 팔을 선호 작업 영역(Preferred Arm Region) 내에 유지하면 이동 중 갑작스러운 회피 동작이 필요한 가능성을 줄일 수 있다.

동적 조작에서는 액추에이터 용량(Actuator Capacity)도 명시적으로 관리해야 한다. 로봇이 경사면을 오르거나 가속할 때 다리 액추에이터가 토크 한계에 가까워지면 로봇 팔 외란을 보상할 수 있는 전신 제어 여유가 감소한다. 마찬가지로 페이로드를 운반하는 로봇 팔 관절은 베이스 움직임을 충분히 보상하지 못할 수 있다. 토크, 속도, 열 상태(Thermal State), 전력 사용률을 감시하면 이동과 로봇 팔의 결합 요구가 하드웨어 성능을 초과하기 전에 조작 강도를 감소시킬 수 있다.

복구 행동(Recovery Behavior)은 로봇 안정성과 조작 안전성을 모두 유지해야 한다. 균형 상태가 악화되면 시스템은 로봇 팔을 몸체 쪽으로 후퇴시키거나 페이로드를 몸통 가까이 이동시키고, 상호작용력을 감소시키거나 필요한 경우 중요도가 낮은 객체를 해제할 수 있다. 접촉 작업에서는 제어되지 않은 로봇 팔 후퇴 자체가 위험을 발생시킬 수 있으므로 복구 과정에서 환경 제약조건도 고려해야 한다. 작업 감독기(Task Supervisor)는 현재 파지, 접촉, 지형, 지지 조건에 따라 적절한 복구 행동을 선택해야 한다.

학습 기반 제어(Learning-Based Control)는 모델 기반 동적 협조(Model-Based Dynamic Coordination)를 보완할 수 있다. 강화학습 정책(Reinforcement Learning Policy)은 수작업으로 설계하기 어려운 보행과 로봇 팔 움직임 사이의 시간적 관계를 학습할 수 있으며, 잔차 정책(Residual Policy)은 모델 오차를 보상할 수 있다. 무작위화된 지형, 페이로드, 접촉 조건, 지연, 외란을 이용하여 학습하면 강건성을 향상시킬 수 있다. 동시에 학습된 행동이 핵심적인 관절, 충돌, 안정성 한계를 위반하지 않도록 결정론적 안전 제약조건(Deterministic Safety Constraint)을 유지해야 한다.

실시간 구현(Real-Time Implementation)에는 여러 제어 주파수가 필요하다. 전신 안정화(Whole-Body Stabilization)와 관절 제어는 일반적으로 높은 주파수에서 동작하고, 궤적 계획, 인지, 지형 분석, 작업 의사결정은 상대적으로 낮은 주파수에서 갱신될 수 있다. 이러한 계층 사이에서는 공통된 타임스탬프와 일관된 로봇 상태 추정값을 사용하는 것이 필수적이다. 동적 이동 중에는 짧은 시간에도 베이스 자세가 크게 변화할 수 있으므로 지연된 로봇 팔 또는 목표물 정보가 특히 심각한 문제를 발생시킬 수 있다.

시뮬레이션(Simulation)에서는 보행 속도, 보행 유형, 로봇 팔 궤적, 페이로드, 지형, 외력, 인지 불확실성의 다양한 조합을 시험해야 한다. 유용한 평가 지표에는 말단장치 추종 오차, 몸체 자세 편차, 발 미끄러짐, 접촉력 여유, 관절 토크, 조작 성공률, 보행 교란, 복구 성능 등이 포함된다. 정지 상태 조작과 점진적으로 빨라지는 이동 중 조작을 비교하면 동역학적 결합이 작업 정확도 또는 안정성을 제한하기 시작하는 조건을 파악할 수 있다.

하드웨어 검증(Hardware Validation)은 저속 보행 중 단순한 로봇 팔 움직임에서 시작하여 더욱 복잡한 협조 작업으로 단계적으로 확장해야 한다. 초기 시험에서는 4족 보행 로봇이 이동하는 동안 손을 월드 좌표계의 고정 자세로 유지하고, 이후 리칭, 운반, 파지, 접촉 상호작용으로 발전시킬 수 있다. 그다음 지형 복잡도와 이동 속도를 점진적으로 증가시킬 수 있다. 육안으로 확인하기 어려운 결합 효과를 식별하기 위해 상태, 접촉, 토크, 궤적, 인지 데이터를 높은 주파수로 기록해야 한다.

동적 이동 중 조작(Manipulation During Dynamic Locomotion)은 궁극적으로 이동 제어와 로봇 팔 제어가 하나의 물리적 행동(Physical Behavior)으로 기능하도록 요구한다. 다리는 지속적으로 변화하는 지지 조건을 생성하고, 몸통은 움직이는 조작 베이스를 제공하며, 로봇 팔은 작업 움직임과 동역학적 반력을 동시에 발생시킨다. 운동량, 접촉력, 보행 위상, 인지, 전신 움직임을 협조함으로써 4족 보행 로봇은 정밀한 상호작용이 필요할 때마다 이동을 완전히 중지하지 않고도 유용한 조작 작업을 수행할 수 있다.

##  

## 09.09. Tool Use with Quadruped Arm [w/Code]

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

Tool use with a quadruped arm extends manipulation from direct object handling to tasks in which the robot controls an external implement to modify or interact with the environment. The tool may be a probe, inspection instrument, brush, scraper, lever, wrench, screwdriver, cutter, or specialized industrial device. Successful operation requires the robot to reason about the tool as an extension of its manipulator rather than treating the gripper itself as the final interaction point.

A tool-use task begins with identifying the tool, its graspable region, functional geometry, and intended interaction mode. The robot must distinguish between the grasp frame used to hold the tool and the task frame associated with the working tip or surface. For a long probe, for example, the relevant task point may be far from the gripper. Accurate knowledge of this transformation is essential because end-effector motion must ultimately produce the desired tool-tip trajectory.

Tool acquisition requires grasp planning that considers both grasp stability and future usability. A mechanically secure grasp may still be unsuitable if it places the tool at an inconvenient orientation or leaves insufficient wrist range for the task. Candidate grasps should therefore be evaluated according to tool alignment, arm manipulability, collision clearance, expected forces, and the workspace required after acquisition. The grasp should support the complete operation rather than only successful pickup.

When tool geometry is known, a predefined tool center point can be registered relative to the gripper. For unfamiliar or uncertain tools, the robot may estimate this relationship using vision, depth sensing, tactile observations, or controlled calibration motions. Small errors in tool length or orientation can produce significant errors at the working point, especially for elongated tools. Online refinement of the tool transform can therefore improve accuracy before precise interaction begins.

The quadruped should establish a base pose that provides sufficient workspace for the complete tool trajectory. Tool use often enlarges the effective manipulation envelope and introduces additional collision constraints beyond those of the bare arm. The robot must consider whether the tool can reach the target, whether the wrist can maintain the required orientation, and whether the legs and trunk can support the expected interaction forces without approaching unstable configurations.

Tool motion is naturally described in task coordinates associated with the functional part of the tool. A screwdriver may require translation along its axis combined with rotation, while a scraper may require motion tangent to a surface with controlled normal force. A probe may require precise point positioning and orientation. Representing commands in the tool task frame allows the controller to express the physical objective directly rather than constructing it indirectly through gripper motion.

Tool use frequently introduces kinematic constraints after environmental contact. Once a tool tip enters a hole, engages a fastener, rests against a surface, or contacts a mechanism, arbitrary Cartesian movement is no longer appropriate. The controller must respect the geometry imposed by the task. Constrained motion can be represented explicitly through allowable directions or inferred from measured force and motion when the exact environmental geometry is uncertain.

Force control becomes essential when task success depends on maintaining contact rather than merely reaching a pose. Brushing, scraping, polishing, probing, tightening, and levering require controlled interaction forces or torques. Excessive force can damage the tool, environment, or robot, while insufficient force may make the operation ineffective. Force-torque sensing at the wrist or estimated joint torques can provide feedback for regulating the interaction.

Impedance control provides useful compliance when the tool or environment geometry is imperfectly known. The controller can maintain stiffness along directions requiring precise guidance while allowing compliant motion along uncertain contact directions. For surface-following tasks, moderate normal compliance can accommodate geometric variation while tangential motion follows the desired path. This prevents small modeling errors from generating large internal forces or causing the tool to lose contact.

Hybrid motion-force control can separate directions requiring trajectory tracking from those requiring force regulation. During surface cleaning, tangential directions can follow a commanded path while normal force is controlled independently. During insertion, axial motion may be commanded while lateral forces guide alignment. Tool-specific coordinate frames make this decomposition easier because controlled directions can be defined according to the physical function of the tool.

Whole-body coordination is important because tool reaction forces propagate from the working point through the tool, gripper, arm, trunk, legs, and ground contacts. A long tool can amplify moments at the wrist and quadruped body. The whole-body controller can redistribute ground reaction forces, adjust trunk posture, or reposition the feet to provide a stronger mechanical support configuration before applying substantial force.

Tool leverage can be beneficial but also increases dynamic sensitivity. A long handle may allow the robot to generate useful torque at a mechanism with moderate gripper force, yet the same lever arm magnifies positioning errors and disturbances. Planning should therefore consider both mechanical advantage and controllability. The preferred grasp location may change depending on whether the task prioritizes large force, precise positioning, or a compromise between the two.

Dynamic tool use introduces additional inertial effects. Rapidly moving a heavy or elongated tool changes whole-body momentum and can disturb locomotion or stance stability. Trajectory generation should limit acceleration and jerk according to tool mass and inertia. If the robot must use a tool while stepping, demanding interaction phases can be synchronized with favorable support conditions, while arm motion can be reduced during vulnerable contact transitions.

Perception should track both the environment and the tool after grasping. The assumed tool pose relative to the gripper can change because of grasp slip, compliance, or mechanical play. Visual tracking of the tool tip or recognizable features can detect these changes. Combining visual measurements with gripper, tactile, and force information allows the robot to maintain a more reliable estimate of the true interaction point throughout the operation.

Collision checking must include the complete tool geometry as soon as it is grasped. A tool may extend significantly beyond the robot\'s normal arm envelope and can collide with the trunk, legs, surrounding equipment, or people even when the manipulator itself is collision-free. Swept-volume prediction is particularly useful for long tools because rotational wrist motion can cause the distant tool tip to move through a large region of space.

Many tool operations consist of repeated motion primitives. Turning a fastener may require rotate, release, reposition, regrasp, and rotate again. Cleaning may require repeated surface strokes, while probing may involve sequential measurement locations. These behaviors can be represented as reusable manipulation primitives coordinated by a task executive. Sensor-based transition conditions should determine when each primitive has succeeded rather than relying only on fixed timing.

Regrasping may be necessary when the original tool grasp cannot provide sufficient workspace for the complete task. The robot can temporarily place the tool, change its grasp, or manipulate it against environmental support to obtain a more useful configuration. Regrasp planning should preserve tool control and avoid unstable intermediate states. For demanding tasks, the quadruped may also reposition its body between tool-use phases instead of relying exclusively on arm motion.

Tool-use planning should include functional success criteria. Reaching the commanded trajectory does not necessarily mean that the task has been completed. A fastener must reach the required state, a surface operation must cover the intended region, and a probe must obtain a valid measurement. Force signatures, visual changes, mechanism state, tool displacement, or sensor readings can provide evidence that the physical objective has actually been achieved.

Tool condition should also be monitored when relevant. Unexpected changes in force, vibration, orientation, or task progress can indicate slipping, jamming, wear, breakage, or incorrect engagement. Continuing to execute the nominal trajectory under these conditions can increase damage. The controller should reduce force, stop motion, withdraw the tool, or initiate another attempt when observed interaction differs substantially from the expected physical behavior.

Recovery is particularly important because tool use introduces additional failure modes beyond ordinary grasping. The robot may fail to acquire the tool, grasp it incorrectly, lose calibration, miss the target, jam the working tip, exceed force limits, or drop the tool. Recovery behavior can include tool reacquisition, pose re-estimation, compliant withdrawal, base repositioning, regrasping, or task termination depending on the detected failure.

Safety supervision should constrain tool-tip speed, interaction wrench, arm torque, body stability, collision distance, and permitted workspace. These limits may depend on tool type because a lightweight inspection probe and a heavy rigid implement create different risks. Safety logic should remain independent of high-level task success and be able to stop or retract the manipulator when unexpected contact, excessive force, or unstable robot motion is detected.

Learning-based methods can complement model-based tool control when interaction dynamics are difficult to specify manually. Demonstration learning or reinforcement learning can acquire tool trajectories, contact strategies, or recovery behaviors from repeated experience. Learned policies can adapt to variation in geometry and friction, while conventional force control and safety constraints preserve predictable physical behavior. Hybrid architectures are therefore attractive for practical deployment.

Simulation can evaluate different tool dimensions, masses, grasp locations, contact properties, target poses, friction conditions, and robot stances before hardware testing. Relevant metrics include tool-tip tracking error, interaction-force error, task completion rate, grasp retention, peak joint torque, collision frequency, stability margin, and recovery success. Hardware validation should progress from lightweight tools and low-force contact toward realistic industrial interaction.

Tool use ultimately expands the functional capability of an arm-equipped quadruped without requiring a dedicated actuator for every possible task. Locomotion positions the robot, whole-body control establishes mechanical support, the arm provides gross tool motion, and compliant contact control regulates the functional interaction point. By combining tool geometry, perception, force reasoning, manipulation planning, and stable mobility, the quadruped can operate a broad range of human-designed implements in complex environments.

4족 보행 로봇 팔을 이용한 도구 사용(Tool Use with a Quadruped Arm)은 로봇의 조작 능력을 직접적인 객체 취급에서 외부 도구를 제어하여 환경을 변화시키거나 상호작용하는 작업으로 확장한다. 도구는 프로브(Probe), 검사 장비, 브러시, 스크레이퍼(Scraper), 레버, 렌치, 스크루드라이버, 절단 도구 또는 특수 산업용 장비일 수 있다. 성공적인 작업을 위해서는 그리퍼 자체를 최종 상호작용 지점으로 취급하는 것이 아니라 도구를 매니퓰레이터(Manipulator)의 연장으로 인식하고 제어해야 한다.

도구 사용 작업(Tool-Use Task)은 도구를 식별하고 파지 가능한 영역, 기능적 형상, 의도된 상호작용 방식을 파악하는 것에서 시작한다. 로봇은 도구를 잡는 데 사용되는 파지 좌표계(Grasp Frame)와 실제 작업 끝단 또는 표면에 대응하는 작업 좌표계(Task Frame)를 구분해야 한다. 예를 들어 긴 프로브의 경우 실제 작업 지점은 그리퍼에서 상당히 멀리 떨어져 있을 수 있다. 말단장치 움직임을 통해 최종적으로 원하는 도구 끝단 궤적을 생성해야 하므로 이러한 변환 관계를 정확하게 파악하는 것이 필수적이다.

도구 획득(Tool Acquisition)을 위한 파지 계획(Grasp Planning)은 파지 안정성과 이후의 사용 가능성을 모두 고려해야 한다. 기계적으로 안정적인 파지라도 도구를 불편한 방향으로 배치하거나 작업 수행에 필요한 손목 가동 범위를 충분히 확보하지 못한다면 적절하지 않을 수 있다. 따라서 후보 파지는 도구 정렬, 로봇 팔 조작성(Arm Manipulability), 충돌 여유, 예상되는 힘, 획득 이후 필요한 작업공간을 기준으로 평가해야 한다. 파지는 단순히 도구를 집는 데 성공하는 것뿐만 아니라 전체 작업을 지원할 수 있어야 한다.

도구 형상이 알려진 경우에는 사전에 정의된 도구 중심점(Tool Center Point)을 그리퍼를 기준으로 등록할 수 있다. 익숙하지 않거나 형상이 불확실한 도구의 경우에는 비전, 깊이 센싱(Depth Sensing), 촉각 관측 또는 제어된 캘리브레이션 동작(Calibration Motion)을 이용하여 이러한 관계를 추정할 수 있다. 특히 길이가 긴 도구에서는 길이나 방향의 작은 오차도 작업 지점에서 큰 위치 오차를 발생시킬 수 있다. 따라서 정밀한 상호작용을 시작하기 전에 도구 변환 관계(Tool Transform)를 온라인으로 보정하면 정확도를 향상시킬 수 있다.

4족 보행 로봇은 전체 도구 궤적을 수행하기에 충분한 작업공간을 제공하는 베이스 자세(Base Pose)를 형성해야 한다. 도구 사용은 일반적으로 유효 조작 범위를 확장하고 로봇 팔 자체만을 사용할 때보다 추가적인 충돌 제약조건을 발생시킨다. 로봇은 도구가 목표물에 도달할 수 있는지, 손목이 필요한 방향을 유지할 수 있는지, 다리와 몸통이 불안정한 자세에 접근하지 않으면서 예상되는 상호작용력을 지지할 수 있는지를 함께 고려해야 한다.

도구 움직임은 기능적인 도구 부분과 연결된 작업 좌표(Task Coordinate)에서 자연스럽게 표현할 수 있다. 스크루드라이버는 축 방향 병진과 회전을 결합해야 할 수 있으며, 스크레이퍼는 제어된 수직력(Normal Force)을 유지하면서 표면의 접선 방향으로 움직여야 할 수 있다. 프로브는 정밀한 지점 위치와 방향 제어가 필요할 수 있다. 명령을 도구 작업 좌표계(Tool Task Frame)에서 표현하면 그리퍼 움직임을 통해 간접적으로 구성하는 대신 실제 물리적 작업 목표를 직접 표현할 수 있다.

도구 사용은 환경과 접촉한 이후 기구학적 제약조건(Kinematic Constraint)을 발생시키는 경우가 많다. 도구 끝단이 구멍에 삽입되거나 체결 부품과 맞물리고, 표면에 놓이거나 기계 장치에 접촉하면 더 이상 임의의 카테시안 운동(Cartesian Motion)을 수행할 수 없다. 제어기는 작업에 의해 결정되는 기하학적 구조를 따라야 한다. 제약 운동(Constrained Motion)은 허용 가능한 움직임 방향으로 명시적으로 표현하거나 정확한 환경 형상을 알 수 없는 경우 측정된 힘과 움직임을 통해 추정할 수 있다.

작업 성공 여부가 단순히 특정 자세에 도달하는 것이 아니라 접촉 유지에 의해 결정되는 경우에는 힘 제어(Force Control)가 필수적이다. 브러싱, 스크레이핑, 폴리싱, 프로빙, 체결, 레버 조작 등은 제어된 상호작용력 또는 토크를 필요로 한다. 과도한 힘은 도구, 환경 또는 로봇을 손상시킬 수 있고, 힘이 부족하면 작업 자체가 효과적으로 수행되지 않을 수 있다. 손목의 힘-토크 센싱(Force-Torque Sensing) 또는 추정된 관절 토크를 이용하여 상호작용력을 조절하기 위한 피드백을 제공할 수 있다.

임피던스 제어(Impedance Control)는 도구 또는 환경의 기하학적 형상을 정확하게 알 수 없는 경우 유용한 순응성(Compliance)을 제공한다. 제어기는 정밀한 유도가 필요한 방향에는 충분한 강성(Stiffness)을 유지하면서 불확실한 접촉 방향에는 순응 움직임을 허용할 수 있다. 표면 추종 작업(Surface-Following Task)에서는 적절한 수직 방향 순응성을 이용하여 기하학적 변화를 수용하면서 접선 방향으로 원하는 경로를 추종할 수 있다. 이를 통해 작은 모델링 오차가 큰 내부 힘을 발생시키거나 도구가 접촉을 잃는 것을 방지할 수 있다.

하이브리드 운동-힘 제어(Hybrid Motion-Force Control)는 궤적 추종이 필요한 방향과 힘 조절이 필요한 방향을 분리할 수 있다. 표면 청소 작업에서는 접선 방향으로 명령된 경로를 추종하면서 수직 방향 힘을 독립적으로 제어할 수 있다. 삽입 작업에서는 축 방향 운동을 명령하면서 측면 힘을 이용하여 정렬을 유도할 수 있다. 도구별 좌표계(Tool-Specific Coordinate Frame)를 사용하면 실제 도구의 물리적 기능을 기준으로 제어 방향을 정의할 수 있으므로 이러한 분리가 더욱 용이해진다.

도구의 반력이 작업 지점에서 도구, 그리퍼, 로봇 팔, 몸통, 다리, 지면 접촉으로 전달되므로 전신 협조(Whole-Body Coordination)가 중요하다. 긴 도구는 손목과 4족 보행 로봇 몸체에 작용하는 모멘트를 증가시킬 수 있다. 전신 제어기(Whole-Body Controller)는 상당한 힘을 가하기 전에 지면 반력(Ground Reaction Force)을 재분배하고 몸통 자세를 조정하거나 발 위치를 변경하여 더욱 강한 기계적 지지 구성을 형성할 수 있다.

도구의 레버리지(Tool Leverage)는 유용하지만 동역학적 민감성도 증가시킨다. 긴 손잡이를 사용하면 비교적 작은 그리퍼 힘으로 기계 장치에 유용한 토크를 발생시킬 수 있지만, 동일한 레버 암(Lever Arm)은 위치 오차와 외란도 확대한다. 따라서 계획 과정에서는 기계적 이점(Mechanical Advantage)과 제어 가능성을 모두 고려해야 한다. 작업에서 큰 힘, 정밀한 위치 결정 또는 이 둘의 절충 중 무엇을 우선하는지에 따라 적절한 파지 위치가 달라질 수 있다.

동적인 도구 사용(Dynamic Tool Use)은 추가적인 관성 효과를 발생시킨다. 무겁거나 길이가 긴 도구를 빠르게 움직이면 전신 운동량(Whole-Body Momentum)이 변화하여 이동 또는 지지 안정성을 교란할 수 있다. 궤적 생성(Trajectory Generation)에서는 도구의 질량과 관성에 따라 가속도와 저크(Jerk)를 제한해야 한다. 로봇이 스테핑 중 도구를 사용해야 한다면 높은 상호작용력이 요구되는 구간을 유리한 지지 조건과 동기화하고, 취약한 접촉 전환 과정에서는 로봇 팔 움직임을 감소시킬 수 있다.

도구를 파지한 이후에도 인지 시스템(Perception System)은 환경과 도구를 모두 추적해야 한다. 그리퍼를 기준으로 가정한 도구 자세는 파지 미끄러짐, 순응성 또는 기계적 유격으로 인해 변화할 수 있다. 도구 끝단이나 인식 가능한 특징에 대한 시각 추적(Visual Tracking)을 이용하면 이러한 변화를 감지할 수 있다. 시각 측정값과 그리퍼, 촉각, 힘 정보를 결합하면 작업 전체에서 실제 상호작용 지점의 자세를 더욱 신뢰성 있게 추정할 수 있다.

도구를 파지하는 즉시 전체 도구 형상을 충돌 검사(Collision Checking)에 포함해야 한다. 도구는 로봇 팔의 일반적인 작업 영역을 크게 벗어날 수 있으며, 매니퓰레이터 자체에는 충돌이 없더라도 몸통, 다리, 주변 설비 또는 사람과 충돌할 수 있다. 특히 긴 도구에서는 손목의 회전 움직임으로 멀리 떨어진 도구 끝단이 넓은 공간을 통과할 수 있으므로 스윕 볼륨 예측(Swept-Volume Prediction)이 유용하다.

많은 도구 작업은 반복적인 운동 프리미티브(Motion Primitive)로 구성된다. 체결 부품을 돌리는 작업은 회전, 해제, 재배치, 재파지, 다시 회전하는 과정을 요구할 수 있다. 청소 작업은 반복적인 표면 스트로크(Surface Stroke)를 필요로 하며, 프로빙 작업은 여러 측정 위치를 순차적으로 검사할 수 있다. 이러한 행동은 작업 실행기(Task Executive)가 협조하는 재사용 가능한 조작 프리미티브(Manipulation Primitive)로 표현할 수 있다. 각 프리미티브의 성공 여부는 고정된 시간에만 의존하지 않고 센서 기반 전환 조건에 따라 결정해야 한다.

초기의 도구 파지가 전체 작업을 수행하기에 충분한 작업공간을 제공하지 못하면 재파지(Regrasping)가 필요할 수 있다. 로봇은 도구를 일시적으로 내려놓고 파지 위치를 변경하거나 환경의 지지 구조를 활용하여 보다 유리한 자세로 도구를 조작할 수 있다. 재파지 계획은 도구에 대한 제어를 유지하면서 불안정한 중간 상태를 피해야 한다. 높은 난이도의 작업에서는 로봇 팔 움직임에만 의존하지 않고 도구 사용 단계 사이에 4족 보행 로봇의 몸체 자체를 재배치할 수도 있다.

도구 사용 계획(Tool-Use Planning)은 기능적인 성공 기준(Functional Success Criteria)을 포함해야 한다. 명령된 궤적을 추종했다는 사실만으로 작업이 완료되었다고 판단할 수 없다. 체결 부품은 요구되는 상태까지 도달해야 하고, 표면 작업은 지정된 영역을 충분히 처리해야 하며, 프로브는 유효한 측정값을 획득해야 한다. 힘의 특성, 시각적 변화, 메커니즘 상태, 도구 변위 또는 센서 측정값을 이용하여 실제 물리적 목표가 달성되었는지 판단할 수 있다.

필요한 경우 도구 상태(Tool Condition)도 지속적으로 감시해야 한다. 힘, 진동, 방향 또는 작업 진행 상태에서 예상하지 못한 변화가 나타나면 미끄러짐, 걸림(Jamming), 마모, 파손 또는 잘못된 결합 상태를 의미할 수 있다. 이러한 조건에서 기존 궤적을 계속 실행하면 손상 가능성이 증가한다. 관측된 상호작용이 예상되는 물리적 동작과 크게 다를 경우 제어기는 힘을 줄이고 움직임을 정지하거나 도구를 후퇴시킨 후 새로운 시도를 시작해야 한다.

도구 사용에는 일반적인 파지보다 더 많은 실패 형태가 존재하기 때문에 복구(Recovery)가 특히 중요하다. 로봇은 도구 획득에 실패하거나 잘못된 위치를 파지하고, 캘리브레이션 정보를 잃거나, 목표물을 놓치고, 작업 끝단이 걸리거나, 힘 한계를 초과하거나, 도구를 떨어뜨릴 수 있다. 감지된 실패 유형에 따라 도구 재획득, 자세 재추정, 순응 후퇴(Compliant Withdrawal), 베이스 재배치, 재파지 또는 작업 종료 등의 복구 행동을 수행할 수 있다.

안전 감독(Safety Supervision)은 도구 끝단 속도, 상호작용 렌치(Interaction Wrench), 로봇 팔 토크, 몸체 안정성, 충돌 거리, 허용 작업공간을 제한해야 한다. 이러한 한계는 도구 유형에 따라 달라질 수 있으며, 가벼운 검사 프로브와 무겁고 단단한 작업 도구는 서로 다른 위험을 발생시킨다. 안전 로직은 상위 작업의 성공 여부와 독립적으로 유지되어야 하며 예상하지 못한 접촉, 과도한 힘 또는 불안정한 로봇 움직임이 감지되면 매니퓰레이터를 정지하거나 후퇴시킬 수 있어야 한다.

학습 기반 방법(Learning-Based Method)은 상호작용 동역학을 수작업으로 정의하기 어려운 경우 모델 기반 도구 제어(Model-Based Tool Control)를 보완할 수 있다. 시연 학습(Demonstration Learning) 또는 강화학습(Reinforcement Learning)을 이용하여 반복 경험으로부터 도구 궤적, 접촉 전략 또는 복구 행동을 학습할 수 있다. 학습 정책은 형상과 마찰 변화에 적응하고, 기존의 힘 제어와 안전 제약조건은 예측 가능한 물리적 동작을 유지할 수 있다. 따라서 하이브리드 구조(Hybrid Architecture)는 실제 시스템 적용에 적합한 방법이 될 수 있다.

시뮬레이션(Simulation)을 이용하면 하드웨어 시험 전에 다양한 도구 크기, 질량, 파지 위치, 접촉 특성, 목표 자세, 마찰 조건, 로봇 지지 자세를 평가할 수 있다. 주요 성능 지표에는 도구 끝단 추종 오차, 상호작용력 오차, 작업 완료율, 파지 유지 성능, 최대 관절 토크, 충돌 빈도, 안정성 여유, 복구 성공률 등이 포함된다. 하드웨어 검증(Hardware Validation)은 가벼운 도구와 저하중 접촉에서 시작하여 실제 산업 환경의 상호작용으로 단계적으로 확장해야 한다.

도구 사용(Tool Use)은 궁극적으로 가능한 모든 작업마다 전용 액추에이터를 장착하지 않고도 로봇 팔을 가진 4족 보행 로봇의 기능적 능력을 크게 확장한다. 이동(Locomotion)은 로봇의 작업 위치를 결정하고, 전신 제어(Whole-Body Control)는 기계적 지지 기반을 형성하며, 로봇 팔은 도구의 전체적인 움직임을 생성하고, 순응 접촉 제어(Compliant Contact Control)는 실제 기능적 상호작용 지점을 조절한다. 도구 형상, 인지, 힘 추론(Force Reasoning), 조작 계획, 안정적인 이동을 통합함으로써 4족 보행 로봇은 복잡한 환경에서 사람이 사용하도록 설계된 다양한 도구를 효과적으로 운용할 수 있다.

##  

## 09.10. Quadruped Manipulation Industrial Case Study

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

Industrial quadruped manipulation combines legged mobility with physical interaction so that a robot can perform useful work in facilities that were originally designed for human operators. Unlike conventional industrial manipulators fixed to a workstation, an arm-equipped quadruped can traverse stairs, uneven floors, narrow passages, platforms, and distributed work areas before performing manipulation. This mobility enables one robotic platform to service multiple locations without dedicated automation infrastructure.

A representative industrial mission begins with autonomous deployment from a charging or staging area to a remote work location. The quadruped navigates corridors, equipment zones, ramps, stairs, and partially structured terrain while maintaining localization and obstacle awareness. The manipulator normally remains in a compact transport configuration during navigation to reduce collision risk, joint loading, and dynamic disturbance until the robot approaches the designated manipulation area.

The industrial task can involve inspection followed by physical intervention. For example, the robot may navigate to a process unit, inspect gauges and thermal conditions, identify an abnormal state, and then operate a valve, switch, lever, or access panel. This sequence demonstrates an important advantage of mobile manipulation: perception does not merely generate a report but can trigger a controlled physical action that changes the state of the industrial environment.

Before manipulation begins, the robot establishes a task-compatible base pose. Navigation accuracy alone is not sufficient because the final body configuration must provide arm reachability, camera visibility, collision clearance, and mechanical support. The robot can refine its position using local perception and adjust individual footholds or trunk posture. A stable manipulation stance increases available end-effector force and reduces the likelihood that arm motion will destabilize the quadruped.

Local perception identifies the target mechanism and estimates its task-relevant geometry. RGB, depth, thermal, or other inspection sensors may locate handles, valves, switches, connectors, instruments, and surrounding structures. The manipulation system converts these observations into target frames for grasping and interaction. Close-range sensing is particularly important because global facility maps rarely contain the precise mechanism pose required for reliable physical manipulation.

A valve-operation case illustrates contact-rich industrial manipulation. The robot aligns its gripper with the valve, establishes a secure grasp, and applies controlled torque while monitoring force and motion. The valve constrains the hand to a particular rotational path, so the controller must follow the mechanism rather than impose an arbitrary Cartesian trajectory. If the required rotation exceeds the arm workspace, the robot can release, reposition, regrasp, and continue the operation.

Whole-body control becomes critical when the task generates substantial reaction forces. Torque applied to a valve or force applied to a lever propagates through the manipulator into the trunk and stance legs. The controller can redistribute ground reaction forces, modify body posture, and adjust support geometry to resist this wrench. Manipulation feasibility therefore depends not only on arm strength but also on the mechanical configuration of the entire quadruped.

Another industrial case is opening an equipment door or access panel before inspection or maintenance. The robot detects and grasps the handle, operates the latch, and follows the door trajectory while maintaining contact. As the door rotates, the required hand position moves outside the initial arm workspace. The quadruped may need to step or reposition its trunk while preserving the grasp, transforming a simple arm task into coordinated locomotion and manipulation.

Tool use further expands the industrial mission. The robot can acquire an inspection probe, cleaning tool, wrench, or specialized end-effector and transport it to a work location. After grasping, the tool becomes part of the effective manipulation geometry. The system must track the tool center point, account for additional mass and inertia, include the tool in collision checking, and regulate the interaction forces appropriate for its functional operation.

Payload handling provides another practical application. A quadruped can collect a component, sample container, maintenance item, or replacement part and transport it across terrain inaccessible to conventional wheeled manipulators. The payload changes the combined center of mass and dynamic response of the robot, requiring adjustments to gait, body posture, and arm configuration. During difficult traversal, the object can be held close to the trunk to reduce destabilizing moments.

At the destination, the robot transitions from transport to precision placement. Local perception estimates the receiving fixture, shelf, container, or work surface, while the quadruped chooses a base pose that provides suitable reachability. Visual servoing can correct residual alignment error, and compliant control can detect physical contact. The object is released only after the system verifies that the destination provides stable support and that the payload will remain in the intended configuration.

Industrial environments frequently contain constrained spaces that make collision management essential. Pipes, handrails, cabinets, machinery, cables, and structural members can surround the manipulation target. Collision checking must include the arm, legs, trunk, payload, and any grasped tool. Because the robot may change posture or step during manipulation, collision geometry should be updated continuously rather than evaluated only when the initial manipulation trajectory is generated.

Autonomous task execution can be organized through a state machine or behavior tree that coordinates navigation, inspection, manipulation, verification, and recovery. Each transition should depend on observed physical state rather than elapsed time alone. A valve command, for example, should not be considered successful merely because the arm executed the planned rotation. Sensor feedback should confirm that the mechanism actually moved to the required state.

Industrial reliability requires explicit recovery behavior. The robot may arrive at an unsuitable stance, fail to detect the target, miss a grasp, encounter unexpectedly high mechanism resistance, lose localization, or reach a joint limit. Recovery can include local repositioning, perception reinitialization, alternative grasp selection, compliant withdrawal, regrasping, or route replanning. When autonomous recovery is not safe, the robot should transition to a controlled state for operator assistance.

Human supervision remains valuable even when most of the mission is autonomous. An operator can authorize high-consequence actions, provide task-level commands, inspect sensor data, or intervene when environmental conditions fall outside validated operating limits. The preferred architecture keeps continuous low-level balance and force control onboard while allowing supervisory decisions to occur remotely. Communication loss should not compromise basic stability or manipulation safety.

Safety supervision should operate independently of task completion logic. Joint torque, end-effector force, gripper load, body attitude, foot contact, collision distance, actuator temperature, and payload condition can be monitored continuously. When limits are approached, the system can reduce speed, stop manipulation, retract the arm, or adopt a stable posture. Industrial autonomy should fail safely rather than repeatedly forcing a mechanism when the physical state is uncertain.

Industrial deployment also requires consideration of communication, computing, and power availability. Perception, state estimation, locomotion, whole-body control, and safety-critical manipulation should remain functional on the robot when network connectivity is degraded. Remote infrastructure can support mission planning, fleet coordination, data storage, and model updates, but essential physical control should not depend on unpredictable network latency.

Operational data from each mission can support continuous system improvement. Logs can include robot state, camera observations, force measurements, joint torque, contact events, task transitions, operator interventions, and failure conditions. Repeated analysis reveals which mechanisms, terrain conditions, or manipulation phases cause difficulty. These observations can guide controller tuning, perception improvements, new recovery behaviors, and targeted simulation scenarios.

Simulation provides a scalable environment for reproducing industrial tasks before deployment. Digital representations of equipment, terrain, mechanisms, payloads, and obstacles can be combined with variations in friction, object pose, sensor noise, and interaction resistance. Simulation is particularly useful for testing rare failures that would be expensive or hazardous to reproduce repeatedly on physical equipment, although final validation must still include representative hardware interaction.

Performance evaluation should measure the complete mission rather than only manipulation accuracy. Relevant metrics include navigation success, time to reach the task, target detection rate, grasp success, mechanism-operation success, placement accuracy, peak interaction force, number of recovery attempts, energy consumption, operator intervention frequency, and total mission completion rate. Long-duration repeated trials are necessary to expose reliability problems that may not appear in isolated demonstrations.

A staged deployment strategy reduces integration risk. Initial operation can use supervised navigation and simple low-force manipulation in controlled industrial areas. Subsequent stages can introduce autonomous navigation, contact-rich mechanisms, payload transport, tool use, stairs, and increasingly complex terrain. Each stage should have measurable acceptance criteria so that new capabilities are added only after the underlying locomotion, perception, manipulation, and safety functions demonstrate sufficient reliability.

The industrial value of quadruped manipulation is strongest where mobility and physical intervention must occur together. Fixed robots provide excellent repeatability inside structured cells, while wheeled mobile manipulators are efficient on accessible floors. Arm-equipped quadrupeds address a different operating space: distributed facilities containing stairs, irregular terrain, obstacles, and human-oriented equipment where a robot must first reach the task and then physically interact with it.

An industrial quadruped manipulation system therefore represents more than a walking robot carrying an arm. It integrates autonomous navigation, terrain adaptation, perception, whole-body control, grasping, force interaction, tool use, payload handling, recovery, and safety supervision into a single operational platform. When these capabilities are validated as an integrated system, the quadruped can progress from remote inspection toward autonomous physical work in hazardous, remote, and infrastructure-constrained industrial environments.

산업용 4족 보행 로봇 조작(Industrial Quadruped Manipulation)은 보행 이동성과 물리적 상호작용을 결합하여 원래 사람 작업자를 위해 설계된 산업 시설에서도 로봇이 실질적인 작업을 수행할 수 있도록 한다. 작업장에 고정된 기존 산업용 매니퓰레이터(Industrial Manipulator)와 달리 로봇 팔을 장착한 4족 보행 로봇은 조작 작업을 수행하기 전에 계단, 불규칙한 바닥, 좁은 통로, 플랫폼, 분산된 작업 구역을 이동할 수 있다. 이러한 이동성은 전용 자동화 인프라 없이 하나의 로봇 플랫폼이 여러 작업 위치를 담당할 수 있도록 한다.

대표적인 산업 임무(Industrial Mission)는 충전 또는 대기 구역에서 원격 작업 위치까지 자율적으로 이동하는 과정에서 시작된다. 4족 보행 로봇은 위치 추정(Localization)과 장애물 인식(Obstacle Awareness)을 유지하면서 복도, 설비 구역, 경사로, 계단, 부분적으로 구조화된 지형을 이동한다. 매니퓰레이터는 일반적으로 로봇이 지정된 조작 영역에 접근할 때까지 충돌 위험, 관절 부하, 동역학적 외란을 줄이기 위해 몸체 가까이에 접힌 운송 자세(Compact Transport Configuration)를 유지한다.

산업 작업은 검사(Inspection) 이후 물리적인 개입(Physical Intervention)을 수행하는 형태로 구성될 수 있다. 예를 들어 로봇은 공정 설비로 이동하여 계기와 열 상태를 검사하고, 비정상 상태를 식별한 다음 밸브, 스위치, 레버 또는 접근 패널을 조작할 수 있다. 이러한 작업 순서는 이동 조작(Mobile Manipulation)의 중요한 장점을 보여준다. 즉, 인지 시스템(Perception System)이 단순히 검사 보고서를 생성하는 데 그치지 않고 산업 환경의 상태를 실제로 변화시키는 제어된 물리적 행동을 실행할 수 있다.

조작을 시작하기 전에 로봇은 작업에 적합한 베이스 자세(Task-Compatible Base Pose)를 형성해야 한다. 최종 몸체 구성은 로봇 팔의 도달 가능성, 카메라 가시성, 충돌 여유, 기계적 지지 능력을 제공해야 하므로 내비게이션 정확도만으로는 충분하지 않다. 로봇은 국부 인지(Local Perception)를 이용하여 자신의 위치를 정밀하게 보정하고 개별 발 위치 또는 몸통 자세를 조정할 수 있다. 안정적인 조작 자세는 사용 가능한 말단장치 힘을 증가시키고 로봇 팔 움직임으로 인해 4족 보행 로봇이 불안정해질 가능성을 감소시킨다.

국부 인지는 목표 메커니즘(Target Mechanism)을 식별하고 작업과 관련된 기하학적 형상을 추정한다. RGB, 깊이(Depth), 열화상(Thermal) 또는 기타 검사 센서를 이용하여 손잡이, 밸브, 스위치, 커넥터, 계기 및 주변 구조물을 탐지할 수 있다. 조작 시스템은 이러한 관측값을 파지와 상호작용을 위한 목표 좌표계(Target Frame)로 변환한다. 전역 시설 지도에는 신뢰성 있는 물리적 조작에 필요한 정확한 메커니즘 자세가 포함되어 있지 않은 경우가 많기 때문에 근거리 센싱(Close-Range Sensing)이 특히 중요하다.

밸브 조작 사례(Valve-Operation Case)는 접촉 중심 산업 조작(Contact-Rich Industrial Manipulation)을 잘 보여준다. 로봇은 그리퍼를 밸브에 정렬하고 안정적인 파지를 형성한 후 힘과 움직임을 감시하면서 제어된 토크를 가한다. 밸브는 손의 움직임을 특정 회전 경로로 제한하므로 제어기는 임의의 카테시안 궤적(Cartesian Trajectory)을 강제하는 대신 실제 메커니즘의 움직임을 따라야 한다. 필요한 회전량이 로봇 팔 작업공간을 초과하면 로봇은 파지를 해제하고 위치를 변경한 후 다시 파지하여 작업을 계속할 수 있다.

작업에서 상당한 반력이 발생하면 전신 제어(Whole-Body Control)가 핵심적인 역할을 한다. 밸브에 가해지는 토크 또는 레버에 가해지는 힘은 매니퓰레이터를 통해 몸통과 지지 다리로 전달된다. 제어기는 이러한 렌치(Wrench)에 대응하기 위해 지면 반력(Ground Reaction Force)을 재분배하고 몸체 자세를 변경하며 지지 형상을 조정할 수 있다. 따라서 조작 가능성은 로봇 팔의 힘만으로 결정되는 것이 아니라 4족 보행 로봇 전체의 기계적 구성에 의해 결정된다.

또 다른 산업 사례는 검사 또는 유지보수 전에 장비 도어(Equipment Door)나 접근 패널(Access Panel)을 여는 작업이다. 로봇은 손잡이를 탐지하고 파지한 다음 래치를 작동시키고 접촉을 유지하면서 문의 궤적을 따라간다. 문이 회전하면 필요한 손의 위치가 초기 로봇 팔 작업공간을 벗어날 수 있다. 이 경우 4족 보행 로봇은 파지를 유지하면서 스테핑하거나 몸통 위치를 변경해야 하며, 단순한 로봇 팔 작업은 이동과 조작이 협조된 작업으로 확장된다.

도구 사용(Tool Use)은 산업 임무의 범위를 더욱 확장한다. 로봇은 검사 프로브(Inspection Probe), 청소 도구, 렌치 또는 특수 말단장치를 획득하여 작업 위치까지 운반할 수 있다. 도구를 파지하면 해당 도구는 실질적인 조작 형상의 일부가 된다. 시스템은 도구 중심점(Tool Center Point)을 추적하고 추가된 질량과 관성을 고려하며, 도구 형상을 충돌 검사에 포함하고, 도구의 기능적 작업에 적합한 상호작용력을 조절해야 한다.

페이로드 취급(Payload Handling)은 또 다른 실용적인 응용 분야이다. 4족 보행 로봇은 부품, 샘플 용기, 유지보수 물품 또는 교체 부품을 획득하여 기존의 바퀴형 매니퓰레이터가 접근하기 어려운 지형을 통과해 운송할 수 있다. 페이로드는 로봇의 결합 질량중심(Combined Center of Mass)과 동역학적 응답을 변화시키므로 보행, 몸체 자세, 로봇 팔 구성의 조정이 필요하다. 어려운 지형을 이동할 때에는 객체를 몸통 가까이에 유지하여 불안정성을 유발하는 모멘트를 감소시킬 수 있다.

목적지에 도착하면 로봇은 운송 모드에서 정밀 배치(Precision Placement)로 전환한다. 국부 인지는 물품을 받을 고정구, 선반, 용기 또는 작업 표면의 자세를 추정하고, 4족 보행 로봇은 적절한 도달 가능성을 제공하는 베이스 자세를 선택한다. 시각 서보잉(Visual Servoing)을 이용하여 남아 있는 정렬 오차를 보정하고 순응 제어(Compliant Control)를 이용하여 물리적 접촉을 감지할 수 있다. 목적지가 페이로드를 안정적으로 지지하며 객체가 의도한 자세를 유지한다는 것을 확인한 후에만 객체를 해제해야 한다.

산업 환경에는 제한된 공간이 많기 때문에 충돌 관리(Collision Management)가 필수적이다. 배관, 난간, 캐비닛, 기계 장비, 케이블, 구조물이 조작 목표 주변에 존재할 수 있다. 충돌 검사에는 로봇 팔뿐만 아니라 다리, 몸통, 페이로드, 파지한 도구까지 포함해야 한다. 로봇이 조작 과정에서 자세를 변경하거나 스테핑할 수 있으므로 충돌 형상은 초기 조작 궤적을 생성할 때 한 번만 평가하는 것이 아니라 지속적으로 갱신해야 한다.

자율 작업 실행(Autonomous Task Execution)은 내비게이션, 검사, 조작, 검증, 복구를 협조하는 상태 머신(State Machine) 또는 행동 트리(Behavior Tree)를 통해 구성할 수 있다. 각각의 상태 전환은 단순한 경과 시간이 아니라 관측된 실제 물리적 상태에 따라 결정해야 한다. 예를 들어 로봇 팔이 계획된 회전을 수행했다는 이유만으로 밸브 작업이 성공했다고 판단해서는 안 된다. 센서 피드백을 이용하여 메커니즘이 실제로 요구된 상태까지 이동했는지 확인해야 한다.

산업 환경에서 요구되는 신뢰성(Industrial Reliability)을 확보하려면 명시적인 복구 행동(Recovery Behavior)이 필요하다. 로봇은 부적절한 자세로 작업 위치에 도착하거나, 목표물을 탐지하지 못하거나, 파지에 실패하거나, 예상보다 높은 메커니즘 저항을 만나거나, 위치 추정을 잃거나, 관절 한계에 도달할 수 있다. 복구 과정에는 국부 재배치, 인지 재초기화, 대체 파지 선택, 순응 후퇴(Compliant Withdrawal), 재파지 또는 경로 재계획이 포함될 수 있다. 자율 복구가 안전하지 않은 경우에는 작업자의 지원을 받을 수 있는 제어된 상태로 전환해야 한다.

대부분의 임무가 자율적으로 수행되더라도 사람의 감독(Human Supervision)은 여전히 중요한 역할을 한다. 작업자는 결과에 큰 영향을 미치는 행동을 승인하고, 작업 수준의 명령을 제공하거나, 센서 데이터를 검사하고, 환경 조건이 검증된 운용 한계를 벗어난 경우 개입할 수 있다. 바람직한 구조에서는 지속적인 저수준 균형 제어와 힘 제어를 로봇 내부에서 수행하고 상위 수준의 감독 의사결정은 원격에서 수행할 수 있다. 통신이 끊어지더라도 기본적인 안정성과 조작 안전성이 손상되어서는 안 된다.

안전 감독(Safety Supervision)은 작업 완료 로직과 독립적으로 동작해야 한다. 관절 토크, 말단장치 힘, 그리퍼 하중, 몸체 자세, 발 접촉, 충돌 거리, 액추에이터 온도, 페이로드 상태 등을 지속적으로 감시할 수 있다. 이러한 한계에 접근하면 시스템은 속도를 낮추고 조작을 정지하거나 로봇 팔을 후퇴시키고 안정적인 자세를 취할 수 있다. 산업용 자율 시스템(Industrial Autonomous System)은 물리적 상태가 불확실할 때 메커니즘에 반복적으로 힘을 가하는 대신 안전한 상태로 전환되어야 한다.

산업 현장 배치(Industrial Deployment)에서는 통신, 컴퓨팅, 전력 가용성도 고려해야 한다. 네트워크 연결 상태가 저하되더라도 인지, 상태 추정, 이동, 전신 제어, 안전에 중요한 조작 기능은 로봇 자체에서 계속 동작할 수 있어야 한다. 원격 인프라는 임무 계획, 플릿 협조(Fleet Coordination), 데이터 저장, 모델 업데이트를 지원할 수 있지만 핵심적인 물리 제어 기능이 예측할 수 없는 네트워크 지연에 의존해서는 안 된다.

각 임무에서 수집된 운용 데이터(Operational Data)는 시스템의 지속적인 개선에 활용할 수 있다. 로그에는 로봇 상태, 카메라 관측, 힘 측정값, 관절 토크, 접촉 이벤트, 작업 상태 전환, 작업자 개입, 실패 조건 등을 포함할 수 있다. 반복적인 분석을 통해 어떤 메커니즘, 지형 조건 또는 조작 단계에서 어려움이 발생하는지 파악할 수 있다. 이러한 관측 결과는 제어기 튜닝, 인지 성능 개선, 새로운 복구 행동 설계, 표적화된 시뮬레이션 시나리오 구성에 활용할 수 있다.

시뮬레이션(Simulation)은 실제 배치 전에 산업 작업을 재현할 수 있는 확장 가능한 환경을 제공한다. 장비, 지형, 메커니즘, 페이로드, 장애물의 디지털 표현을 마찰, 객체 자세, 센서 잡음, 상호작용 저항 등의 변화와 결합할 수 있다. 특히 실제 장비에서 반복적으로 재현하기에는 비용이 높거나 위험한 희귀 실패 상황을 시험하는 데 시뮬레이션이 유용하다. 그러나 최종적인 검증에는 실제 운용 조건을 대표할 수 있는 하드웨어 상호작용(Hardware Interaction)이 반드시 포함되어야 한다.

성능 평가(Performance Evaluation)는 단순한 조작 정확도가 아니라 전체 임무를 대상으로 수행해야 한다. 관련 지표에는 내비게이션 성공률, 작업 위치 도달 시간, 목표 탐지율, 파지 성공률, 메커니즘 조작 성공률, 배치 정확도, 최대 상호작용력, 복구 시도 횟수, 에너지 소비, 작업자 개입 빈도, 전체 임무 완료율 등이 포함된다. 개별적인 시연에서는 나타나지 않는 신뢰성 문제를 발견하려면 장시간 반복 시험(Long-Duration Repeated Trial)이 필요하다.

단계적 배치 전략(Staged Deployment Strategy)은 시스템 통합 위험을 감소시킨다. 초기 운용에서는 통제된 산업 구역에서 감독형 내비게이션(Supervised Navigation)과 단순한 저하중 조작을 사용할 수 있다. 이후 단계에서는 자율 내비게이션, 접촉 중심 메커니즘, 페이로드 운송, 도구 사용, 계단, 더욱 복잡한 지형을 점진적으로 도입할 수 있다. 각각의 단계에는 측정 가능한 승인 기준(Acceptance Criteria)을 설정하여 기반이 되는 이동, 인지, 조작, 안전 기능이 충분한 신뢰성을 입증한 이후에만 새로운 기능을 추가해야 한다.

4족 보행 로봇 조작의 산업적 가치(Industrial Value)는 이동성과 물리적 개입이 동시에 요구되는 환경에서 가장 크게 나타난다. 고정형 로봇은 구조화된 작업 셀에서 뛰어난 반복 정밀도를 제공하고, 바퀴형 이동 매니퓰레이터(Wheeled Mobile Manipulator)는 접근 가능한 평탄한 바닥에서 높은 효율성을 제공한다. 로봇 팔을 장착한 4족 보행 로봇은 이와 다른 운용 영역을 담당한다. 즉, 계단, 불규칙한 지형, 장애물, 사람 중심으로 설계된 설비가 존재하며 로봇이 먼저 작업 위치에 도달한 후 물리적으로 상호작용해야 하는 분산형 시설에 적합하다.

따라서 산업용 4족 보행 로봇 조작 시스템(Industrial Quadruped Manipulation System)은 단순히 로봇 팔을 장착한 보행 로봇 이상의 의미를 가진다. 자율 내비게이션, 지형 적응(Terrain Adaptation), 인지, 전신 제어, 파지, 힘 상호작용(Force Interaction), 도구 사용, 페이로드 취급, 복구, 안전 감독을 하나의 운용 플랫폼으로 통합한다. 이러한 기능들이 통합 시스템으로 충분히 검증되면 4족 보행 로봇은 원격 검사(Remote Inspection)를 넘어 위험하고 원격에 위치하며 인프라 제약이 존재하는 산업 환경에서 자율적인 물리 작업(Autonomous Physical Work)을 수행하는 플랫폼으로 발전할 수 있다.
