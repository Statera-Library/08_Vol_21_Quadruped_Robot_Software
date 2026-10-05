**Volume 21. Quadruped Robot Software**


# Chapter 01. Quadruped Robot Fundamentals

##  

## 01.01. Quadruped Robot Morphology and Design Space

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

Quadruped robot morphology defines the physical organization of a four-legged robotic system and establishes the mechanical foundation on which locomotion, perception, control, and autonomy are built. Unlike wheeled robots, quadrupeds interact with the environment through discrete and continuously changing contact points. Their body geometry, limb arrangement, joint structure, actuator placement, and mass distribution therefore directly determine mobility, stability, energy efficiency, and terrain adaptability.

The fundamental morphology consists of a central trunk and four articulated legs positioned around the body. The trunk normally carries batteries, computing hardware, communication devices, inertial sensors, and payloads, while the legs generate supporting and propulsive forces. The relative dimensions of the trunk and legs determine the reachable workspace of each foot, achievable ground clearance, support polygon geometry, turning capability, and ability to negotiate obstacles.

A quadruped leg is commonly represented as a serial kinematic chain containing approximately three active degrees of freedom. A typical configuration includes hip abduction-adduction, hip flexion-extension, and knee flexion-extension. These joints allow the foot to move through a three-dimensional workspace rather than merely swinging forward and backward. Additional degrees of freedom may improve dexterity, but they also increase actuator count, mechanical complexity, control dimensionality, mass, and energy consumption.

Leg geometry strongly influences locomotion characteristics. Longer legs can provide greater obstacle clearance, larger reachable foothold regions, and potentially longer strides, but they also increase bending moments and structural loads. Shorter legs generally provide higher structural stiffness and a lower center of mass, although they restrict terrain negotiation. Designers therefore select link lengths by balancing desired speed, payload capacity, obstacle dimensions, actuator capability, structural strength, and overall robot size.

The orientation of the knee joints creates another important morphological choice. Legs may use forward-facing, backward-facing, symmetric, or mixed knee configurations depending on the intended workspace and mechanical packaging. Knee orientation changes the distribution of feasible foot positions and can influence collision avoidance between the legs and body. It also affects how effectively joint torques can be transformed into ground reaction forces under different postures and terrain conditions.

Body dimensions determine both static geometry and dynamic behavior. A longer body can increase separation between front and rear contacts and provide additional payload space, while a wider body can enlarge lateral support geometry. Excessive dimensions, however, increase rotational inertia and reduce maneuverability in confined environments. Compact bodies improve turning and accessibility but create tighter packaging constraints for batteries, computers, actuators, thermal systems, and payload interfaces.

Mass distribution is especially important because locomotion continuously accelerates and decelerates both the trunk and limbs. Concentrating heavy components near the body center reduces rotational inertia and generally improves dynamic responsiveness. Batteries and major computing hardware are therefore commonly positioned inside the trunk. Keeping distal leg segments lightweight reduces swing inertia, allowing faster foot repositioning while lowering actuator torque requirements and impact-related loads.

Actuator placement is closely coupled with morphology. Directly placing motors at individual joints produces mechanically straightforward transmission paths but increases distal limb mass. Alternatively, actuators can be located closer to the trunk and connected through belts, gears, linkages, cables, or other transmissions. Proximal actuator placement can significantly reduce leg inertia, although additional transmission components introduce compliance, friction, backlash, packaging constraints, and maintenance considerations.

The foot forms the final mechanical interface between the robot and terrain. Its dimensions, shape, compliance, friction characteristics, and sensing capability influence traction and impact behavior. Small rigid feet provide accurate contact geometry on firm surfaces but can generate high local pressure. Larger or compliant feet distribute forces more broadly and accommodate uneven surfaces. Specialized designs may incorporate elastomers, force sensors, tactile sensing, or replaceable terrain-specific contact materials.

Morphology must also account for the robot\'s center of mass relative to its support contacts. During slow locomotion, stability can often be understood through the geometric relationship between the projected center of mass and the support polygon. During dynamic locomotion, momentum, acceleration, ground reaction forces, and contact timing become equally important. Consequently, morphology should not be optimized only for standing stability; it must support the intended dynamic behaviors and control strategies.

The quadruped design space includes important trade-offs among speed, payload, endurance, terrain capability, and mechanical robustness. A lightweight robot with powerful actuators may achieve rapid dynamic locomotion but sacrifice operating time or payload. A heavy platform optimized for transportation may provide excellent load capacity but require substantially larger actuators and batteries. No single morphology is optimal because different operational missions impose fundamentally different combinations of constraints.

Terrain requirements provide one of the strongest drivers of morphological selection. Robots designed for indoor floors can use relatively compact legs and limited foot clearance, whereas outdoor platforms may require longer limbs, larger joint ranges, greater ground clearance, and stronger structures. Rubble, stairs, slopes, vegetation, rocks, mud, and discontinuous terrain each impose different requirements on reachable footholds, foot design, joint torque, sensing placement, and mechanical protection.

Joint range of motion defines the geometric envelope within which the robot can reposition its feet and body. Large ranges enable deep crouching, high stepping, recovery maneuvers, body orientation adjustment, and adaptation to irregular surfaces. However, extreme ranges can create singular configurations, self-collision risks, cable-routing difficulties, and reduced structural stiffness. Practical designs therefore coordinate mechanical joint limits with the useful regions of the kinematic workspace.

Structural compliance introduces another dimension into quadruped morphology. Highly rigid mechanisms simplify geometric modeling and provide accurate motion transmission, while compliant structures can absorb impacts and store mechanical energy. Compliance may originate from elastic feet, flexible links, series elastic actuators, or transmission elements. Properly designed compliance can improve robustness and energy efficiency, but excessive or poorly modeled flexibility can reduce positioning accuracy and complicate feedback control.

Sensor placement must be considered during mechanical design rather than treated as an independent subsystem. Inertial measurement units benefit from rigid mounting near representative body locations, while cameras and LiDAR require unobstructed fields of view and protection from impacts. Joint encoders, motor current sensing, foot force sensors, and contact sensors provide proprioceptive information. Morphology therefore determines not only how the robot moves but also how effectively it observes its own physical state.

Thermal management and environmental protection further constrain the design space. High-performance actuators, power electronics, batteries, and onboard computers generate substantial heat inside a compact body. Sealed housings required for dust or water resistance can make cooling more difficult. Designers must reserve volume for heat sinks, airflow paths, conductive structures, connectors, seals, and protective covers without significantly increasing mass or interfering with leg motion.

Payload integration changes the effective morphology of the complete robot. Manipulators, inspection equipment, communication modules, cargo, or specialized sensors alter the center of mass, inertia, power consumption, and structural loading. A morphology optimized only for the unloaded platform may perform poorly after payload installation. Payload interfaces should therefore be considered as part of the original mechanical architecture, including allowable mass, mounting location, power supply, communication, and dynamic loading.

Scale also changes the underlying engineering problem. Small quadrupeds can use relatively lightweight structures and compact actuators, whereas large robots experience rapidly increasing structural loads, impact forces, and power requirements. Simply enlarging an existing design does not preserve its performance. Link cross-sections, bearings, transmissions, thermal capacity, battery energy, actuator torque density, and foot-ground pressure must all be reconsidered when moving between different size and payload classes.

Modern quadruped design increasingly treats morphology and control as a coupled optimization problem. Mechanical geometry determines the feasible motion space, while control algorithms determine how effectively that space can be exploited. Simulation and optimization can evaluate combinations of link lengths, body dimensions, actuator capabilities, joint limits, foot properties, and mass distributions against mission-level objectives such as speed, stability, energy consumption, payload, or terrain traversal.

This relationship becomes even more important in learning-based locomotion. Reinforcement learning policies can discover motions that exploit subtle mechanical properties such as compliance, inertia, and contact geometry, but they remain constrained by the physical platform. Poor morphology cannot simply be compensated for by a more sophisticated controller. Conversely, a well-designed mechanical structure can enlarge the feasible behavior space and reduce the control effort required to achieve robust locomotion.

Quadruped morphology should therefore be understood as a system-level design problem rather than a selection of isolated mechanical dimensions. Body geometry, leg topology, actuators, transmissions, feet, sensors, batteries, computing hardware, payloads, thermal design, and environmental protection interact with one another. Effective design requires evaluating these relationships together so that the resulting robot provides an appropriate physical foundation for perception, locomotion, manipulation, and autonomous operation.

사족보행 로봇 형태학(Quadruped Robot Morphology)은 네 개의 다리를 가진 로봇 시스템의 물리적 구성을 정의하며, 보행(Locomotion), 인식(Perception), 제어(Control), 자율성(Autonomy)이 구현되는 기계적 기반을 형성한다. 바퀴형 로봇(Wheeled Robot)과 달리 사족보행 로봇은 이산적이며 지속적으로 변화하는 접촉점(Contact Point)을 통해 환경과 상호작용한다. 따라서 몸체 형상, 다리 배치, 관절 구조, 액추에이터(Actuator) 배치 및 질량 분포는 이동성, 안정성, 에너지 효율 및 지형 적응성을 직접 결정한다.

기본적인 형태학(Morphology)은 중앙 몸체(Central Trunk)와 몸체 주변에 배치된 네 개의 관절형 다리(Articulated Leg)로 구성된다. 몸체에는 일반적으로 배터리, 컴퓨팅 하드웨어, 통신 장치, 관성 센서(Inertial Sensor) 및 탑재물(Payload)이 배치되며, 다리는 지지력과 추진력을 생성한다. 몸체와 다리의 상대적인 크기는 각 발의 도달 작업공간(Reachable Workspace), 확보 가능한 지상고(Ground Clearance), 지지 다각형(Support Polygon)의 형상, 회전 능력 및 장애물 극복 능력을 결정한다.

사족보행 로봇의 다리는 일반적으로 약 세 개의 능동 자유도(Active Degree of Freedom)를 갖는 직렬 운동학 체인(Serial Kinematic Chain)으로 표현된다. 대표적인 구성에는 고관절 외전-내전(Hip Abduction-Adduction), 고관절 굴곡-신전(Hip Flexion-Extension), 무릎 굴곡-신전(Knee Flexion-Extension)이 포함된다. 이러한 관절은 발이 단순히 전후 방향으로 움직이는 것이 아니라 3차원 작업공간(Three-Dimensional Workspace)에서 이동할 수 있도록 한다. 자유도를 추가하면 운동 능력은 향상될 수 있지만 액추에이터 수, 기계적 복잡성, 제어 차원, 질량 및 에너지 소비도 증가한다.

다리 형상(Leg Geometry)은 보행 특성에 큰 영향을 미친다. 긴 다리는 더 높은 장애물 극복 능력, 더 넓은 발 디딤 위치(Foothold) 영역 및 잠재적으로 더 긴 보폭(Stride)을 제공하지만 굽힘 모멘트(Bending Moment)와 구조적 하중을 증가시킨다. 짧은 다리는 일반적으로 더 높은 구조 강성과 낮은 무게중심(Center of Mass)을 제공하지만 지형 극복 능력을 제한한다. 따라서 설계자는 목표 속도, 탑재하중, 장애물 크기, 액추에이터 성능, 구조 강도 및 전체 로봇 크기의 균형을 고려하여 링크 길이(Link Length)를 결정해야 한다.

무릎 관절(Knee Joint)의 방향 역시 중요한 형태학적 설계 선택이다. 다리는 목표 작업공간과 기계적 패키징(Mechanical Packaging)에 따라 전방형, 후방형, 대칭형 또는 혼합형 무릎 구조를 사용할 수 있다. 무릎 방향은 가능한 발 위치의 분포를 변화시키며 다리와 몸체 사이의 충돌 회피(Self-Collision Avoidance)에 영향을 줄 수 있다. 또한 서로 다른 자세와 지형 조건에서 관절 토크(Joint Torque)가 지면 반력(Ground Reaction Force)으로 얼마나 효과적으로 변환되는지에도 영향을 미친다.

몸체 치수(Body Dimension)는 정적 형상뿐만 아니라 동적 거동(Dynamic Behavior)도 결정한다. 긴 몸체는 전방과 후방 접촉점 사이의 거리를 증가시키고 추가적인 탑재 공간을 제공할 수 있으며, 넓은 몸체는 횡방향 지지 영역을 확대할 수 있다. 그러나 지나치게 큰 몸체는 회전 관성(Rotational Inertia)을 증가시키고 제한된 공간에서의 기동성을 감소시킨다. 반대로 소형 몸체는 회전성과 접근성을 향상시키지만 배터리, 컴퓨터, 액추에이터, 열관리 시스템 및 탑재물 인터페이스의 배치 공간을 제한한다.

질량 분포(Mass Distribution)는 보행 과정에서 몸체와 다리가 지속적으로 가속 및 감속되기 때문에 특히 중요하다. 무거운 구성요소를 몸체 중심 부근에 집중시키면 회전 관성을 줄이고 일반적으로 동적 응답성(Dynamic Responsiveness)을 향상시킬 수 있다. 따라서 배터리와 주요 컴퓨팅 하드웨어는 보통 몸체 내부에 배치된다. 다리 말단부(Distal Leg Segment)를 가볍게 유지하면 스윙 관성(Swing Inertia)이 감소하여 발을 더 빠르게 재배치할 수 있으며 액추에이터 토크 요구량과 충격 관련 하중도 감소한다.

액추에이터 배치(Actuator Placement)는 형태학과 밀접하게 결합되어 있다. 각 관절에 모터를 직접 배치하면 동력 전달 경로가 기계적으로 단순해지지만 다리 말단부의 질량이 증가한다. 반대로 액추에이터를 몸체에 가까운 위치에 배치하고 벨트, 기어, 링크, 케이블 또는 기타 전달장치(Transmission)를 통해 동력을 전달할 수 있다. 근위부 액추에이터 배치(Proximal Actuator Placement)는 다리 관성을 크게 감소시킬 수 있지만 추가적인 전달 구성요소로 인해 컴플라이언스(Compliance), 마찰, 백래시(Backlash), 패키징 제약 및 유지보수 문제가 발생할 수 있다.

발(Foot)은 로봇과 지형 사이의 최종적인 기계적 인터페이스(Mechanical Interface)를 형성한다. 발의 크기, 형상, 컴플라이언스, 마찰 특성 및 센싱 능력은 접지력(Traction)과 충격 거동에 영향을 준다. 작고 단단한 발은 견고한 지면에서 정확한 접촉 형상을 제공하지만 높은 국부 압력을 발생시킬 수 있다. 크거나 유연한 발은 힘을 더 넓은 영역에 분산시키고 불규칙한 지면에 적응할 수 있다. 특수 설계에서는 탄성체(Elastomer), 힘 센서(Force Sensor), 촉각 센싱(Tactile Sensing) 또는 교체 가능한 지형별 접촉 재료를 적용할 수 있다.

형태학은 로봇의 무게중심(Center of Mass)과 지지 접촉점(Support Contact) 사이의 관계도 고려해야 한다. 저속 보행에서는 투영된 무게중심(Projected Center of Mass)과 지지 다각형 사이의 기하학적 관계를 통해 안정성을 이해할 수 있다. 동적 보행(Dynamic Locomotion)에서는 운동량, 가속도, 지면 반력 및 접촉 타이밍(Contact Timing)이 동일하게 중요해진다. 따라서 형태학은 정지 상태의 안정성만을 기준으로 최적화해서는 안 되며 목표로 하는 동적 동작과 제어 전략을 지원할 수 있어야 한다.

사족보행 로봇의 설계 공간(Design Space)에는 속도, 탑재하중, 운용시간(Endurance), 지형 주행 능력 및 기계적 강건성(Mechanical Robustness) 사이의 중요한 절충관계(Trade-Off)가 존재한다. 강력한 액추에이터를 탑재한 경량 로봇은 빠른 동적 보행을 구현할 수 있지만 운용시간이나 탑재 능력이 감소할 수 있다. 운송을 목적으로 설계된 중량 플랫폼은 높은 탑재 능력을 제공하지만 훨씬 큰 액추에이터와 배터리가 필요하다. 운용 임무마다 서로 다른 제약조건이 요구되므로 모든 목적에 최적인 단일 형태학은 존재하지 않는다.

지형 요구조건(Terrain Requirement)은 형태학적 설계를 결정하는 가장 강력한 요인 중 하나이다. 실내 평탄면을 대상으로 하는 로봇은 비교적 짧은 다리와 제한적인 발 지상고를 사용할 수 있지만, 실외 플랫폼은 더 긴 다리, 넓은 관절 가동범위(Joint Range), 높은 지상고 및 강한 구조를 요구할 수 있다. 잔해, 계단, 경사면, 식생, 암석, 진흙 및 불연속 지형은 각각 도달 가능한 발 디딤 위치, 발 설계, 관절 토크, 센서 배치 및 기계적 보호에 서로 다른 요구조건을 부여한다.

관절 가동범위(Range of Motion)는 로봇이 발과 몸체를 재배치할 수 있는 기하학적 영역을 정의한다. 넓은 가동범위는 깊은 웅크림(Crouching), 높은 스텝 동작, 자세 복구(Recovery Maneuver), 몸체 방향 조정 및 불규칙 지형 적응을 가능하게 한다. 그러나 지나치게 큰 가동범위는 특이점(Singular Configuration), 자체 충돌 위험, 케이블 배선 문제 및 구조 강성 저하를 발생시킬 수 있다. 따라서 실제 설계에서는 기계적 관절 제한과 유효 운동학 작업공간(Kinematic Workspace)을 함께 고려해야 한다.

구조적 컴플라이언스(Structural Compliance)는 사족보행 로봇 형태학의 또 다른 중요한 설계 요소이다. 높은 강성을 가진 구조는 기하학적 모델링을 단순화하고 정확한 운동 전달을 제공하는 반면, 유연한 구조는 충격을 흡수하고 기계적 에너지를 저장할 수 있다. 컴플라이언스는 탄성 발, 유연한 링크, 직렬 탄성 액추에이터(Series Elastic Actuator) 또는 전달 요소에서 발생할 수 있다. 적절하게 설계된 컴플라이언스는 강건성과 에너지 효율을 향상시키지만 지나치거나 정확하게 모델링되지 않은 유연성은 위치 정확도를 저하시키고 피드백 제어(Feedback Control)를 복잡하게 만든다.

센서 배치(Sensor Placement)는 독립적인 하위 시스템으로 취급하기보다 기계 설계 단계에서 함께 고려해야 한다. 관성측정장치(Inertial Measurement Unit)는 몸체의 대표적인 운동을 측정할 수 있는 강체 위치에 설치하는 것이 유리하며, 카메라와 라이다(LiDAR)는 시야(Field of View)를 확보하면서 충격으로부터 보호되어야 한다. 관절 인코더, 모터 전류 센싱, 발 힘 센서 및 접촉 센서는 고유수용성 정보(Proprioceptive Information)를 제공한다. 따라서 형태학은 로봇의 움직임뿐만 아니라 자신의 물리적 상태를 얼마나 효과적으로 관측할 수 있는지도 결정한다.

열관리(Thermal Management)와 환경 보호(Environmental Protection) 역시 설계 공간을 제한한다. 고성능 액추에이터, 전력전자 장치, 배터리 및 온보드 컴퓨터(Onboard Computer)는 제한된 몸체 내부에서 상당한 열을 발생시킨다. 먼지나 물의 침투를 방지하기 위한 밀폐형 하우징(Sealed Housing)은 냉각을 더욱 어렵게 만들 수 있다. 따라서 설계자는 질량을 과도하게 증가시키거나 다리 운동을 방해하지 않으면서 방열판, 공기 흐름 경로, 열전도 구조, 커넥터, 실링(Sealing) 및 보호 커버를 위한 공간을 확보해야 한다.

탑재물 통합(Payload Integration)은 완성된 로봇 시스템의 실질적인 형태학을 변화시킨다. 매니퓰레이터(Manipulator), 검사 장비, 통신 모듈, 화물 또는 특수 센서는 무게중심, 관성, 전력 소비 및 구조 하중을 변화시킨다. 무부하 플랫폼만을 기준으로 최적화된 형태학은 탑재물 설치 이후 성능이 크게 저하될 수 있다. 따라서 허용 질량, 장착 위치, 전력 공급, 통신 및 동적 하중을 포함하는 탑재물 인터페이스를 초기 기계 아키텍처(Mechanical Architecture)의 일부로 고려해야 한다.

로봇의 크기 규모(Scale)가 달라지면 기본적인 공학 문제 자체도 변화한다. 소형 사족보행 로봇은 비교적 가벼운 구조와 소형 액추에이터를 사용할 수 있지만 대형 로봇에서는 구조 하중, 충격력 및 전력 요구량이 급격하게 증가한다. 기존 설계를 단순히 확대한다고 동일한 성능이 유지되는 것은 아니다. 서로 다른 크기와 탑재하중 등급으로 확장할 때에는 링크 단면, 베어링, 전달장치, 열용량, 배터리 에너지, 액추에이터 토크 밀도(Torque Density) 및 발-지면 압력을 모두 다시 검토해야 한다.

현대의 사족보행 로봇 설계에서는 형태학과 제어를 결합된 최적화 문제(Coupled Optimization Problem)로 다루는 경향이 증가하고 있다. 기계적 형상은 가능한 운동 공간을 결정하고 제어 알고리즘은 이 공간을 얼마나 효과적으로 활용할 수 있는지를 결정한다. 시뮬레이션(Simulation)과 최적화(Optimization)를 통해 링크 길이, 몸체 치수, 액추에이터 성능, 관절 제한, 발 특성 및 질량 분포의 다양한 조합을 속도, 안정성, 에너지 소비, 탑재하중 또는 지형 주행 능력과 같은 임무 수준 목표에 대해 평가할 수 있다.

이러한 관계는 학습 기반 보행(Learning-Based Locomotion)에서 더욱 중요해진다. 강화학습(Reinforcement Learning) 정책은 컴플라이언스, 관성 및 접촉 형상과 같은 미세한 기계적 특성을 활용하는 움직임을 학습할 수 있지만 여전히 물리적 플랫폼의 한계를 벗어날 수 없다. 부적절한 형태학을 더 정교한 제어기만으로 완전히 보상할 수는 없다. 반대로 잘 설계된 기계 구조는 실행 가능한 행동 공간(Feasible Behavior Space)을 확장하고 강건한 보행을 구현하는 데 필요한 제어 부담을 감소시킬 수 있다.

따라서 사족보행 로봇 형태학(Quadruped Robot Morphology)은 개별적인 기계 치수를 선택하는 문제가 아니라 시스템 수준 설계 문제(System-Level Design Problem)로 이해해야 한다. 몸체 형상, 다리 토폴로지(Leg Topology), 액추에이터, 전달장치, 발, 센서, 배터리, 컴퓨팅 하드웨어, 탑재물, 열설계 및 환경 보호 요소는 서로 긴밀하게 상호작용한다. 효과적인 설계는 이러한 관계를 통합적으로 평가함으로써 인식, 보행, 조작(Manipulation) 및 자율 운용(Autonomous Operation)을 위한 적절한 물리적 기반을 제공해야 한다.

##  

## 01.02. Quadruped Kinematics Leg Workspace Reachability [w/Code]

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

Quadruped kinematics describes the geometric relationship between joint motion, leg configuration, body pose, and foot position without directly considering the forces that produce motion. It provides the mathematical foundation for placing each foot at a desired location, generating swing trajectories, maintaining stance contacts, adjusting body posture, and determining whether a commanded foothold can physically be reached by the robot.

A typical quadruped leg is modeled as a serial kinematic chain connected to the trunk through a hip frame. Many practical designs use three actuated joints corresponding to hip abduction-adduction, hip flexion-extension, and knee flexion-extension. Together these joints provide three-dimensional positioning of the foot. The associated link lengths, joint axes, mechanical offsets, and joint limits define the geometric capabilities of each leg.

Kinematic analysis begins by defining coordinate frames for the world, robot body, hip, individual links, and foot. Homogeneous transformations or equivalent rotation and translation representations describe relationships among these frames. By composing transformations from the body toward the foot, the complete pose of the foot can be expressed as a function of the joint variables and known mechanical dimensions of the leg.

Forward kinematics computes the foot position from a known set of joint angles. For a three-degree-of-freedom leg, the joint vector may be written as q = [q1, q2, q3], and a nonlinear mapping produces the Cartesian foot position p = [x, y, z]. Forward kinematics is computationally straightforward and is continuously used for state estimation, visualization, collision checking, contact reasoning, and feedback control.

Inverse kinematics performs the opposite operation by determining joint configurations that place the foot at a desired Cartesian location. This operation is fundamental to locomotion because higher-level planners usually specify desired footholds or foot trajectories rather than individual joint angles. Depending on the geometry, inverse kinematics may have analytical solutions, numerical solutions, multiple valid configurations, or no physically feasible solution for a particular target.

Analytical inverse kinematics is attractive for conventional three-degree-of-freedom quadruped legs because it can provide fast and deterministic computation. Geometric relationships involving link lengths and target coordinates can often be reduced to trigonometric equations. However, a mathematical solution is not automatically a valid physical configuration. Joint limits, knee orientation, self-collision, actuator constraints, and mechanical interference must also be checked before accepting a solution.

The workspace of a leg is the set of foot positions that can be produced by allowable joint configurations. Its shape depends on link lengths, joint-axis arrangement, joint limits, body interference, and mechanical construction. Although idealized kinematic models may produce relatively simple geometric regions, the practical workspace is usually irregular because portions are removed by collision constraints, singularities, limited joint motion, and structural packaging.

Reachability describes whether a specific target position belongs to the feasible workspace. A geometrically reachable point satisfies the kinematic equations for at least one allowable joint configuration. Practical reachability imposes additional conditions, including collision-free motion, sufficient joint torque, acceptable manipulability, contact orientation, and safety margins from joint limits. Therefore, geometric reachability should be distinguished from dynamically usable reachability during locomotion.

The maximum extension of a leg provides only a crude estimate of reachability. Operating continuously near full extension is undesirable because the leg approaches configurations with poor mechanical leverage and reduced ability to generate motion in certain directions. Similarly, highly folded configurations can create collisions and unfavorable force transmission. Locomotion controllers therefore normally define a preferred operating region located well inside the theoretical workspace boundary.

The Jacobian provides a local relationship between joint velocities and Cartesian foot velocity. In simplified form, foot velocity can be expressed as v = J(q)q̇, where J(q) is the configuration-dependent Jacobian matrix. The transpose of the Jacobian also relates Cartesian forces to joint torques. Consequently, the Jacobian connects geometric kinematics with velocity control, force control, impedance control, and whole-body control.

Singularities occur when the Jacobian loses rank and the leg loses the ability to generate arbitrary Cartesian velocity in one or more directions. Near a singularity, small desired foot motions may require very large joint velocities, and Cartesian force commands may produce unfavorable joint torques. Fully extended or specially aligned link configurations frequently approach such conditions. Robust controllers therefore maintain margins from singular regions whenever possible.

Manipulability measures provide a more continuous description of how effectively a leg can move or exert forces around a particular configuration. Instead of asking only whether a point is reachable, manipulability evaluates the directional quality of motion transmission. A foothold deep inside the geometric workspace may still be undesirable if the associated configuration has poor manipulability. This concept is valuable when selecting footholds for dynamic or force-intensive locomotion.

Each of the four legs has its own workspace relative to its corresponding hip frame. When transformed into the body coordinate system, these workspaces define the regions around the robot where each foot can establish contact. The front and rear legs may have similar mechanical structures but different effective operating regions because their mounting orientations differ. Left-right symmetry can simplify modeling, although calibration errors and payload effects can introduce asymmetry.

The body pose strongly influences world-frame reachability. When the trunk translates, rotates, pitches, or rolls, the hip frames move relative to the terrain and the available foothold regions move with them. A foothold that is unreachable from one body pose may become reachable after shifting the body. This coupling between body pose and leg workspace is fundamental to rough-terrain locomotion, stair climbing, gap crossing, and posture adjustment.

During stance, the kinematic relationship can be interpreted in the opposite direction. If a foot is assumed to remain fixed on the ground, changes in joint angles constrain the motion of the body relative to that contact. With multiple stance feet, several simultaneous contact constraints restrict trunk motion. Whole-body controllers exploit these relationships to regulate body position and orientation while distributing motion and forces among the supporting legs.

During swing, the foot moves through free space from one contact location to another. A swing trajectory must remain inside the leg workspace throughout the motion rather than merely having reachable start and end points. It must also provide sufficient terrain clearance and avoid collisions with the body, other legs, and obstacles. Kinematic trajectory generation therefore evaluates intermediate configurations while respecting joint position, velocity, and acceleration limits.

Reachability becomes particularly important in foothold planning. A terrain perception system may identify many geometrically safe contact locations, but only a subset can be reached from the predicted robot state. The planner can intersect terrain-valid regions with leg-reachable regions to produce feasible foothold candidates. Additional criteria such as friction, surface orientation, stability, manipulability, energy cost, and future-step feasibility can then rank these candidates.

A useful distinction exists between instantaneous workspace and locomotion workspace. Instantaneous workspace describes what a leg can reach from the current body configuration, whereas locomotion workspace considers how body movement and sequential contacts expand feasible motion over time. Quadrupeds can therefore traverse distances far beyond the reach of any individual leg by repeatedly transferring support, repositioning the trunk, and establishing new contacts.

Workspace margins are essential for robust locomotion because modeling and sensing are never exact. Joint encoder offsets, link-length tolerances, structural deformation, terrain estimation errors, actuator tracking errors, and contact uncertainty can all reduce practical reachability. Controllers typically shrink the theoretical workspace by safety margins so that commanded foot positions remain feasible despite these uncertainties and leave room for corrective movements after unexpected disturbances.

Calibration directly affects kinematic accuracy. Small errors in link lengths, joint zero positions, joint-axis orientations, or hip mounting locations accumulate through the kinematic chain and appear as foot-position errors. These errors can degrade contact estimation, terrain adaptation, and force control. Accurate quadruped systems therefore combine mechanical measurement, encoder calibration, parameter identification, and sometimes external sensing to refine the kinematic model.

Kinematic redundancy appears when the robot is considered as a complete multi-legged system rather than as four independent three-joint mechanisms. The body pose and multiple leg joints together provide many possible configurations for achieving a locomotion objective. This redundancy can be exploited to avoid joint limits, improve manipulability, maintain sensor orientation, reduce energy consumption, increase stability, or satisfy additional constraints while preserving required foot contacts.

Numerical optimization becomes useful when simple analytical inverse kinematics is insufficient. An optimization-based solver can simultaneously consider desired foot positions, body pose, joint limits, collision constraints, workspace margins, posture preferences, and smoothness. Such formulations naturally extend toward whole-body inverse kinematics and model-based control, although they require careful numerical conditioning and sufficiently fast computation for real-time robotic operation.

For quadruped locomotion, reachability should ultimately be treated as a time-dependent feasibility problem rather than a static geometric test. The future body pose, expected terrain contacts, joint motion limits, swing duration, and subsequent steps determine whether a foothold remains useful. A location that is reachable now may create an unfavorable configuration for the next step, while a slightly less aggressive foothold may preserve significantly greater future mobility.

Kinematics, workspace, and reachability therefore form a central bridge between mechanical design and locomotion intelligence. Link geometry determines the theoretical motion envelope, while sensing, planning, and control decide how that envelope is used. Reliable quadruped systems combine accurate forward and inverse kinematics, Jacobian analysis, singularity avoidance, workspace constraints, calibration, and predictive foothold reasoning to transform desired body motion into physically feasible leg behavior.

사족보행 로봇 운동학(Quadruped Kinematics)은 운동을 발생시키는 힘을 직접 고려하지 않고 관절 운동(Joint Motion), 다리 구성(Leg Configuration), 몸체 자세(Body Pose), 발 위치(Foot Position) 사이의 기하학적 관계를 설명한다. 이는 각 발을 원하는 위치에 배치하고, 스윙 궤적(Swing Trajectory)을 생성하며, 스탠스 접촉(Stance Contact)을 유지하고, 몸체 자세를 조정하며, 명령된 발 디딤 위치(Foothold)가 로봇의 물리적 구조에서 실제로 도달 가능한지를 판단하기 위한 수학적 기반을 제공한다.

일반적인 사족보행 로봇의 다리는 고관절 프레임(Hip Frame)을 통해 몸체에 연결된 직렬 운동학 체인(Serial Kinematic Chain)으로 모델링된다. 많은 실제 설계에서는 고관절 외전-내전(Hip Abduction-Adduction), 고관절 굴곡-신전(Hip Flexion-Extension), 무릎 굴곡-신전(Knee Flexion-Extension)에 해당하는 세 개의 구동 관절을 사용한다. 이러한 관절들은 함께 발의 3차원 위치 제어를 가능하게 하며, 링크 길이, 관절축, 기계적 오프셋 및 관절 제한이 각 다리의 기하학적 운동 능력을 결정한다.

운동학 해석(Kinematic Analysis)은 월드 좌표계(World Frame), 로봇 몸체 좌표계(Body Frame), 고관절 좌표계(Hip Frame), 개별 링크 좌표계(Link Frame), 발 좌표계(Foot Frame)를 정의하는 것에서 시작한다. 동차 변환(Homogeneous Transformation) 또는 이에 상응하는 회전 및 병진 표현을 이용하여 이들 좌표계 사이의 관계를 기술한다. 몸체에서 발 방향으로 변환을 연속적으로 결합하면 발의 전체 자세를 관절 변수와 알려진 다리의 기계적 치수에 대한 함수로 표현할 수 있다.

순기구학(Forward Kinematics)은 주어진 관절 각도로부터 발의 위치를 계산한다. 3자유도(Three-Degree-of-Freedom) 다리의 경우 관절 벡터를 q = [q1, q2, q3]로 나타낼 수 있으며, 비선형 매핑(Nonlinear Mapping)을 통해 직교좌표계 발 위치 p = [x, y, z]를 계산한다. 순기구학은 계산이 비교적 간단하며 상태 추정(State Estimation), 시각화, 충돌 검사(Collision Checking), 접촉 판단(Contact Reasoning), 피드백 제어(Feedback Control)에 지속적으로 사용된다.

역기구학(Inverse Kinematics)은 반대로 원하는 직교좌표 위치에 발을 배치하기 위한 관절 구성을 계산한다. 상위 수준 플래너(High-Level Planner)는 일반적으로 개별 관절 각도보다 원하는 발 디딤 위치 또는 발 궤적을 지정하기 때문에 역기구학은 보행에서 핵심적인 역할을 한다. 다리의 기하학적 구조에 따라 역기구학은 해석적 해(Analytical Solution), 수치적 해(Numerical Solution), 여러 개의 유효한 해를 가질 수 있으며 특정 목표점에 대해서는 물리적으로 가능한 해가 존재하지 않을 수도 있다.

해석적 역기구학(Analytical Inverse Kinematics)은 일반적인 3자유도 사족보행 로봇 다리에 대해 빠르고 결정론적인 계산을 제공할 수 있다는 장점이 있다. 링크 길이와 목표 좌표 사이의 기하학적 관계를 삼각함수 방정식(Trigonometric Equation)으로 변환하여 해를 구할 수 있다. 그러나 수학적으로 계산된 해가 자동으로 유효한 물리적 자세가 되는 것은 아니다. 해를 채택하기 전에 관절 제한, 무릎 방향, 자체 충돌(Self-Collision), 액추에이터 제약 및 기계적 간섭을 함께 검사해야 한다.

다리 작업공간(Leg Workspace)은 허용된 관절 구성을 이용하여 발이 도달할 수 있는 모든 위치의 집합이다. 작업공간의 형상은 링크 길이, 관절축 배치, 관절 제한, 몸체와의 간섭 및 기계적 구조에 따라 결정된다. 이상화된 운동학 모델에서는 비교적 단순한 기하학적 영역이 형성될 수 있지만 실제 작업공간은 충돌 제약, 특이점(Singularity), 제한된 관절 운동 및 구조적 패키징 때문에 일부 영역이 제거되어 일반적으로 불규칙한 형태를 갖는다.

도달 가능성(Reachability)은 특정 목표 위치가 실행 가능한 작업공간(Feasible Workspace)에 포함되는지를 나타낸다. 기하학적으로 도달 가능한 점은 적어도 하나의 허용 가능한 관절 구성에 대해 운동학 방정식을 만족한다. 그러나 실질적인 도달 가능성에는 충돌 없는 움직임, 충분한 관절 토크, 적절한 조작성(Manipulability), 접촉 방향 및 관절 제한으로부터의 안전 여유가 추가로 요구된다. 따라서 기하학적 도달 가능성과 실제 보행 과정에서 동적으로 사용할 수 있는 도달 가능성을 구분해야 한다.

다리의 최대 신장(Maximum Extension)은 도달 가능성을 판단하기 위한 매우 단순한 기준에 불과하다. 다리를 완전히 편 상태에 가까운 영역에서 지속적으로 동작시키는 것은 기계적 지렛대 효과(Mechanical Leverage)가 나빠지고 특정 방향의 운동 생성 능력이 감소하기 때문에 바람직하지 않다. 마찬가지로 지나치게 접힌 자세는 충돌과 불리한 힘 전달을 발생시킬 수 있다. 따라서 보행 제어기(Locomotion Controller)는 일반적으로 이론적인 작업공간 경계보다 충분히 내부에 위치한 선호 동작 영역(Preferred Operating Region)을 정의한다.

자코비안(Jacobian)은 관절 속도와 직교좌표계 발 속도 사이의 국부적인 관계를 제공한다. 단순화하면 발 속도는 v = J(q)q̇로 표현할 수 있으며, 여기에서 J(q)는 현재 관절 구성에 따라 변하는 자코비안 행렬(Jacobian Matrix)이다. 또한 자코비안의 전치행렬(Transpose)은 직교좌표계 힘과 관절 토크 사이의 관계를 나타낸다. 따라서 자코비안은 기하학적 운동학과 속도 제어, 힘 제어, 임피던스 제어(Impedance Control), 전신 제어(Whole-Body Control)를 연결한다.

특이점(Singularity)은 자코비안의 계수(Rank)가 감소하여 다리가 하나 이상의 방향으로 임의의 직교좌표계 속도를 생성할 능력을 상실할 때 발생한다. 특이점 부근에서는 작은 발 움직임을 생성하기 위해 매우 큰 관절 속도가 요구될 수 있으며, 직교좌표계 힘 명령이 불리한 관절 토크를 발생시킬 수 있다. 완전히 신장된 다리 또는 특정 링크들이 정렬된 구성에서 이러한 상태가 자주 발생한다. 따라서 강건한 제어기(Robust Controller)는 가능한 경우 특이 영역으로부터 충분한 여유를 유지한다.

조작성 척도(Manipulability Measure)는 특정 관절 구성 주변에서 다리가 얼마나 효과적으로 움직이거나 힘을 발생시킬 수 있는지를 보다 연속적으로 표현한다. 단순히 특정 점에 도달할 수 있는지를 판단하는 대신 조작성은 운동 전달(Motion Transmission)의 방향별 품질을 평가한다. 발 디딤 위치가 기하학적 작업공간 내부 깊숙한 곳에 있더라도 해당 관절 구성의 조작성이 낮다면 바람직하지 않을 수 있다. 이러한 개념은 동적 보행이나 큰 힘을 요구하는 보행에서 발 디딤 위치를 선택할 때 중요하다.

네 개의 다리는 각각 대응하는 고관절 좌표계를 기준으로 고유한 작업공간을 갖는다. 이러한 작업공간을 몸체 좌표계(Body Coordinate System)로 변환하면 각 발이 로봇 주변에서 접촉할 수 있는 영역을 정의할 수 있다. 전방 다리와 후방 다리는 유사한 기계 구조를 가질 수 있지만 장착 방향이 다르기 때문에 실질적인 동작 영역은 달라질 수 있다. 좌우 대칭(Left-Right Symmetry)은 모델링을 단순화하지만 보정 오차와 탑재물의 영향으로 실제 시스템에서는 비대칭성이 발생할 수 있다.

몸체 자세(Body Pose)는 월드 좌표계 기준의 도달 가능성에 큰 영향을 미친다. 몸체가 병진 이동하거나 회전하고 피치(Pitch) 또는 롤(Roll) 운동을 하면 고관절 좌표계가 지형에 대해 이동하며 사용 가능한 발 디딤 영역도 함께 변화한다. 특정 몸체 자세에서 도달할 수 없는 발 디딤 위치가 몸체를 이동시킨 이후에는 도달 가능해질 수 있다. 이러한 몸체 자세와 다리 작업공간의 결합은 험지 보행, 계단 등반, 간극 통과 및 자세 조정에서 핵심적인 요소이다.

스탠스 단계(Stance Phase)에서는 운동학 관계를 반대 방향으로 해석할 수 있다. 발이 지면에 고정되어 있다고 가정하면 관절 각도의 변화는 해당 접촉점을 기준으로 몸체의 움직임을 제한한다. 여러 개의 발이 동시에 지면을 지지하는 경우 복수의 접촉 제약(Contact Constraint)이 몸체의 움직임을 제한한다. 전신 제어기(Whole-Body Controller)는 이러한 관계를 활용하여 몸체의 위치와 방향을 조절하면서 지지 다리 사이에 움직임과 힘을 적절하게 분배한다.

스윙 단계(Swing Phase)에서는 발이 하나의 접촉 위치에서 다음 접촉 위치까지 자유 공간을 통해 이동한다. 스윙 궤적은 시작점과 끝점만 도달 가능하면 되는 것이 아니라 전체 이동 과정에서 다리 작업공간 내부에 존재해야 한다. 또한 충분한 지형 여유(Terrain Clearance)를 확보하고 몸체, 다른 다리 및 장애물과의 충돌을 피해야 한다. 따라서 운동학적 궤적 생성(Kinematic Trajectory Generation)은 관절 위치, 속도 및 가속도 제한을 만족하면서 중간 관절 구성도 함께 평가해야 한다.

도달 가능성은 발 디딤 계획(Foothold Planning)에서 특히 중요하다. 지형 인식 시스템(Terrain Perception System)이 기하학적으로 안전한 여러 접촉 위치를 탐색하더라도 예측된 로봇 상태에서 실제로 도달할 수 있는 위치는 그중 일부에 불과하다. 플래너는 지형상 유효한 영역과 다리의 도달 가능 영역을 교차하여 실행 가능한 발 디딤 후보를 생성할 수 있다. 이후 마찰, 표면 방향, 안정성, 조작성, 에너지 비용 및 후속 스텝의 실행 가능성과 같은 추가 기준을 사용하여 후보의 우선순위를 결정할 수 있다.

순간 작업공간(Instantaneous Workspace)과 보행 작업공간(Locomotion Workspace)은 서로 구분할 필요가 있다. 순간 작업공간은 현재 몸체 구성에서 한 다리가 도달할 수 있는 영역을 의미하는 반면, 보행 작업공간은 시간에 따른 몸체 이동과 연속적인 접촉 전환을 통해 확장되는 실행 가능한 운동 영역을 의미한다. 따라서 사족보행 로봇은 지지 상태를 반복적으로 전환하고 몸체를 재배치하며 새로운 접촉점을 형성함으로써 개별 다리의 도달 범위를 훨씬 넘어서는 거리를 이동할 수 있다.

작업공간 여유(Workspace Margin)는 모델링과 센싱이 완벽할 수 없기 때문에 강건한 보행을 위해 필수적이다. 관절 인코더 오프셋, 링크 길이 공차, 구조 변형, 지형 추정 오차, 액추에이터 추종 오차 및 접촉 불확실성은 모두 실질적인 도달 가능성을 감소시킬 수 있다. 따라서 제어기는 일반적으로 이론적인 작업공간을 안전 여유만큼 축소하여 발 위치 명령이 이러한 불확실성에도 실행 가능하도록 하고 예상하지 못한 외란(Disturbance)이 발생했을 때 보정 운동을 수행할 수 있는 공간을 확보한다.

보정(Calibration)은 운동학 정확도에 직접적인 영향을 미친다. 링크 길이, 관절 영점(Joint Zero Position), 관절축 방향 또는 고관절 장착 위치의 작은 오차도 운동학 체인을 따라 누적되어 발 위치 오차로 나타난다. 이러한 오차는 접촉 추정, 지형 적응 및 힘 제어 성능을 저하시킬 수 있다. 따라서 정밀한 사족보행 로봇 시스템은 기계적 측정, 인코더 보정(Encoder Calibration), 파라미터 식별(Parameter Identification), 경우에 따라 외부 센싱을 결합하여 운동학 모델을 정교화한다.

운동학적 중복성(Kinematic Redundancy)은 로봇을 서로 독립적인 네 개의 3관절 메커니즘이 아니라 완전한 다족 시스템(Multi-Legged System)으로 고려할 때 나타난다. 몸체 자세와 여러 다리 관절을 함께 사용하면 하나의 보행 목표를 달성할 수 있는 다양한 구성이 존재한다. 이러한 중복성을 활용하여 필요한 발 접촉을 유지하면서 관절 제한을 회피하고, 조작성을 향상시키며, 센서 방향을 유지하고, 에너지 소비를 감소시키거나 안정성을 높이는 등의 추가적인 제약조건을 만족시킬 수 있다.

단순한 해석적 역기구학만으로 충분하지 않은 경우 수치 최적화(Numerical Optimization)가 유용하다. 최적화 기반 해법은 원하는 발 위치, 몸체 자세, 관절 제한, 충돌 제약, 작업공간 여유, 선호 자세 및 움직임의 부드러움(Smoothness)을 동시에 고려할 수 있다. 이러한 공식화는 자연스럽게 전신 역기구학(Whole-Body Inverse Kinematics)과 모델 기반 제어(Model-Based Control)로 확장될 수 있지만 실시간 로봇 운용을 위해서는 적절한 수치적 조건화(Numerical Conditioning)와 충분히 빠른 계산 성능이 필요하다.

사족보행에서 도달 가능성은 궁극적으로 정적인 기하학적 검사보다 시간에 따라 변화하는 실행 가능성 문제(Time-Dependent Feasibility Problem)로 다루어야 한다. 미래의 몸체 자세, 예상 지형 접촉, 관절 운동 제한, 스윙 지속시간 및 이후의 보행 스텝이 특정 발 디딤 위치의 유효성을 결정한다. 현재 도달 가능한 위치라도 다음 스텝에서 불리한 관절 구성을 만들 수 있으며, 조금 덜 공격적인 발 디딤 위치가 이후의 이동 가능성을 훨씬 크게 유지할 수도 있다.

따라서 운동학(Kinematics), 작업공간(Workspace), 도달 가능성(Reachability)은 기계 설계와 보행 지능(Locomotion Intelligence)을 연결하는 핵심적인 가교를 형성한다. 링크 형상은 이론적인 운동 범위를 결정하고 센싱, 계획 및 제어는 이 범위를 실제로 어떻게 활용할지를 결정한다. 신뢰성 높은 사족보행 로봇 시스템은 정확한 순기구학과 역기구학, 자코비안 해석, 특이점 회피, 작업공간 제약, 보정 및 예측 기반 발 디딤 추론(Predictive Foothold Reasoning)을 결합하여 원하는 몸체 움직임을 물리적으로 실행 가능한 다리 동작으로 변환해야 한다.

##  

## 01.03. Quadruped Dynamics Full Body Model [w/Code]

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

Quadruped dynamics describes how forces, torques, inertia, gravity, and ground contacts produce motion of the complete robot. While kinematics determines geometrically possible configurations, dynamics determines whether those motions can physically occur under available actuator and contact forces. A full-body model therefore provides the foundation for balance control, dynamic locomotion, force distribution, trajectory optimization, and whole-body control.

A quadruped is naturally modeled as a floating-base multibody system because its trunk is not permanently attached to the environment. The floating base contributes six degrees of freedom representing three-dimensional translation and rotation, while actuated leg joints contribute additional generalized coordinates. A robot with three actuated joints per leg consequently has twelve actuated joint coordinates combined with the six-dimensional floating-base motion.

The configuration can be represented by generalized coordinates describing body position, body orientation, and joint angles. Generalized velocity similarly contains the linear and angular velocity of the floating base together with joint velocities. Because three-dimensional orientation has special mathematical properties, implementations commonly use rotation matrices or unit quaternions rather than relying exclusively on Euler angles, particularly for large body rotations.

The standard rigid-body dynamics equation can be expressed conceptually as M(q)q̈ + h(q,q̇) = Sᵀτ + Jc(q)ᵀfc. Here M represents the configuration-dependent mass matrix, h contains Coriolis, centrifugal, and gravitational effects, τ represents actuator torques, Jc is the contact Jacobian, and fc contains external contact forces. This equation couples body motion, joint motion, actuation, and environmental interaction.

The mass matrix captures the inertial properties of the complete robot and changes as the legs move relative to the trunk. Its diagonal and off-diagonal terms describe both individual link inertia and dynamic coupling between coordinates. Consequently, accelerating one leg can influence body motion and other joints. Accurate mass, center-of-mass location, and inertia estimates are therefore important for high-performance dynamic locomotion.

Gravity acts on every link and produces configuration-dependent generalized forces. Although gravity appears simple, its effects vary substantially with body orientation, leg posture, and payload distribution. A robot standing on level terrain requires joint torques and ground reaction forces that collectively support its weight, while a robot on a slope must additionally manage tangential loading and altered contact-force distributions.

Coriolis and centrifugal effects become increasingly significant as joint and body velocities rise. During slow walking they may be relatively modest, but during running, jumping, rapid turning, or recovery maneuvers they can strongly influence required actuator torques. Dynamic controllers account for these velocity-dependent terms so that commanded motion reflects the actual coupled behavior of the multibody system rather than an idealized static approximation.

Ground contact fundamentally distinguishes legged dynamics from free-space robotic manipulation. Each stance foot generates ground reaction forces that support and accelerate the robot, while swing feet normally contribute no supporting contact force. Because contacts repeatedly appear and disappear, quadruped dynamics is a hybrid system containing continuous multibody motion separated by discrete events such as touchdown, liftoff, slipping, and impact.

A stance contact imposes constraints on allowable motion. Under an ideal rigid no-slip assumption, the velocity of the contact point relative to the ground is approximately zero. This condition can be expressed through the contact Jacobian and generalized velocity. Differentiating the constraint produces an acceleration-level relationship that can be incorporated into inverse dynamics, constrained dynamics, optimization, and whole-body control formulations.

Ground reaction force must satisfy physical contact conditions. A normal contact force can push the robot away from the surface but cannot pull the ground toward the foot. Tangential forces are limited by available friction and are commonly represented through a friction cone or a linearized friction pyramid. If commanded forces exceed these limits, the foot may slip and the assumed contact model becomes invalid.

The center of mass provides a useful global description of full-body dynamics. Its acceleration is determined by the sum of external forces, primarily gravity and ground reaction forces. Internal joint forces cannot directly accelerate the system center of mass without external interaction. This principle allows complex articulated dynamics to be reduced to simpler centroidal models for many locomotion planning and control problems.

Angular momentum is equally important because the robot must regulate rotational motion of its complete body. Ground reaction forces generate moments around the center of mass depending on their magnitudes and contact locations. Leg motions can also redistribute internal angular momentum. Centroidal dynamics therefore describes both center-of-mass translation and whole-body angular momentum, providing a powerful intermediate model between simplified templates and full rigid-body dynamics.

Simplified dynamic models are often used because solving the complete multibody equations at every planning stage can be computationally expensive. The single rigid body model treats the robot trunk and overall mass as one rigid object acted upon by contact forces. This approximation neglects detailed leg inertia but often captures the dominant dynamics sufficiently well for model predictive control, foothold planning, and ground reaction force optimization.

The full-body model becomes important when limb inertia, rapid leg motion, payloads, manipulation, or aggressive maneuvers cannot be neglected. It explicitly represents individual links, joints, inertial parameters, actuator torques, and contact constraints. Such models allow controllers to calculate dynamically consistent joint commands while considering the effects of leg acceleration, body motion, gravity compensation, and multiple simultaneous contacts.

Inverse dynamics calculates the generalized forces or actuator torques required to realize a desired acceleration while satisfying contact constraints. In quadrupeds, this problem is usually under additional constraints because the floating base is not directly actuated. Body acceleration must instead be generated through forces transmitted by stance legs. Optimization-based inverse dynamics can distribute these forces while respecting friction, torque, and contact limitations.

Forward dynamics performs the complementary calculation. Given the current configuration, velocity, actuator torques, and external forces, it computes the resulting generalized acceleration. Forward dynamics is fundamental to physics simulation because it predicts how the robot evolves under applied commands. It is also useful for controller validation, system identification, reinforcement learning, trajectory prediction, and evaluation of disturbance responses.

The floating base creates an important distinction between actuated and unactuated coordinates. Motors directly generate torque only at the joints, not at the six body coordinates. The trunk can accelerate only through gravity and external forces, especially forces transmitted through stance contacts. Consequently, maintaining body position and orientation requires coordinated leg actuation that creates an appropriate distribution of contact forces across the supporting feet.

Contact-force distribution is generally not unique when several feet support the robot simultaneously. Many combinations of individual foot forces can produce the same desired net force and moment on the body. Controllers exploit this redundancy to minimize energy, avoid actuator saturation, maintain friction margins, balance loads among legs, or preserve robustness. Optimization provides a systematic method for selecting a desirable force distribution.

Actuator limits impose direct constraints on achievable dynamics. Motors and transmissions have finite torque, speed, power, and thermal capability. A motion may be kinematically reachable yet dynamically infeasible because the required joint torque exceeds actuator capacity. Dynamic feasibility must therefore be evaluated together with joint limits, contact friction, battery power, transmission efficiency, and thermal constraints when designing locomotion behaviors.

Impact dynamics becomes important at foot touchdown. Even when a swing foot approaches the terrain with moderate velocity, contact can produce rapid changes in velocity and large impulsive forces. Compliance in the foot, transmission, structure, or controller can reduce impact severity. Accurate touchdown timing and velocity regulation are therefore essential for reducing mechanical stress, preventing rebound, maintaining traction, and improving state-estimation consistency.

Payloads modify the full-body dynamics by changing total mass, center-of-mass position, inertia, and required contact forces. A payload mounted above or away from the body center can substantially increase rotational moments and reduce stability margins. Manipulator motion mounted on the quadruped creates additional time-varying inertial effects. Full-body modeling is therefore particularly important for mobile manipulation and load-carrying applications.

Model accuracy depends on the quality of inertial and actuator parameters. Link masses, centers of mass, inertia tensors, joint friction, transmission characteristics, and motor torque constants may differ from nominal computer-aided design values. System identification can estimate these parameters from measured motion, torque, current, and force data. Improved parameter estimates increase prediction accuracy and reduce systematic errors in model-based controllers.

Real robots also contain dynamics that ideal rigid-body equations do not fully represent. Gearbox backlash, structural flexibility, cable forces, actuator latency, motor saturation, foot compliance, terrain deformation, and unmodeled friction can create discrepancies between prediction and observation. Robust control, feedback correction, disturbance estimation, and adaptive techniques are therefore used alongside physical models rather than relying on perfect mathematical accuracy.

The choice of dynamic model depends on the control layer and computational objective. Simplified models are valuable for fast prediction over longer horizons, while full-body models are valuable for accurate short-horizon control and torque generation. Modern quadruped architectures frequently combine both approaches, using reduced-order dynamics for planning and model predictive control while employing full-body optimization or inverse dynamics for low-level execution.

A full-body dynamic model ultimately connects desired locomotion behavior with physically realizable forces and torques. It explains how actuator commands propagate through articulated limbs, how contacts accelerate and stabilize the floating body, and how inertia and momentum evolve during motion. Reliable quadruped control therefore depends on combining multibody dynamics, contact constraints, friction models, actuator limits, state estimation, and optimization into a coherent physical framework.

사족보행 로봇 동역학(Quadruped Dynamics)은 힘, 토크, 관성, 중력 및 지면 접촉이 전체 로봇의 움직임을 어떻게 발생시키는지를 설명한다. 운동학(Kinematics)이 기하학적으로 가능한 구성을 결정한다면, 동역학(Dynamics)은 사용 가능한 액추에이터(Actuator) 및 접촉력(Contact Force) 조건에서 해당 움직임이 물리적으로 실현 가능한지를 결정한다. 따라서 전신 모델(Full-Body Model)은 균형 제어(Balance Control), 동적 보행(Dynamic Locomotion), 힘 분배(Force Distribution), 궤적 최적화(Trajectory Optimization) 및 전신 제어(Whole-Body Control)의 기반을 제공한다.

사족보행 로봇은 몸체가 환경에 영구적으로 고정되어 있지 않기 때문에 자연스럽게 부동 베이스 다물체 시스템(Floating-Base Multibody System)으로 모델링된다. 부동 베이스(Floating Base)는 3차원 병진 운동과 회전 운동을 나타내는 6자유도(Degree of Freedom)를 가지며, 구동되는 다리 관절은 추가적인 일반화 좌표(Generalized Coordinate)를 제공한다. 따라서 다리당 세 개의 구동 관절을 갖는 로봇은 12개의 구동 관절 좌표와 6차원의 부동 베이스 운동을 함께 갖는다.

로봇의 구성(Configuration)은 몸체 위치, 몸체 방향 및 관절 각도를 나타내는 일반화 좌표로 표현할 수 있다. 일반화 속도(Generalized Velocity)는 이와 유사하게 부동 베이스의 선속도 및 각속도와 관절 속도를 포함한다. 3차원 방향은 특별한 수학적 특성을 가지므로 실제 구현에서는 특히 큰 몸체 회전을 처리할 때 오일러 각(Euler Angle)에만 의존하기보다 회전 행렬(Rotation Matrix)이나 단위 쿼터니언(Unit Quaternion)을 일반적으로 사용한다.

표준 강체 동역학 방정식(Rigid-Body Dynamics Equation)은 개념적으로 M(q)q̈ + h(q,q̇) = Sᵀτ + Jc(q)ᵀfc로 표현할 수 있다. 여기에서 M은 구성에 따라 변하는 질량 행렬(Mass Matrix), h는 코리올리 효과(Coriolis Effect), 원심 효과(Centrifugal Effect) 및 중력 효과를 포함하는 항, τ는 액추에이터 토크, Jc는 접촉 자코비안(Contact Jacobian), fc는 외부 접촉력을 나타낸다. 이 방정식은 몸체 운동, 관절 운동, 구동 및 환경과의 상호작용을 서로 결합한다.

질량 행렬(Mass Matrix)은 전체 로봇의 관성 특성을 나타내며 다리가 몸체에 대해 움직임에 따라 변화한다. 질량 행렬의 대각 및 비대각 항은 개별 링크의 관성뿐만 아니라 좌표 사이의 동적 결합(Dynamic Coupling)을 나타낸다. 따라서 하나의 다리를 가속하면 몸체 움직임과 다른 관절에도 영향을 줄 수 있다. 그러므로 고성능 동적 보행을 구현하기 위해서는 정확한 질량, 무게중심(Center of Mass) 위치 및 관성 추정이 중요하다.

중력(Gravity)은 모든 링크에 작용하며 구성에 따라 변화하는 일반화 힘(Generalized Force)을 발생시킨다. 중력 자체는 단순해 보이지만 그 영향은 몸체 방향, 다리 자세 및 탑재물(Payload) 분포에 따라 크게 달라진다. 평탄한 지면에 서 있는 로봇은 자신의 무게를 지지하기 위해 관절 토크와 지면 반력(Ground Reaction Force)을 함께 사용해야 하며, 경사면에서는 접선 방향 하중과 변화된 접촉력 분포를 추가로 관리해야 한다.

코리올리 효과(Coriolis Effect)와 원심 효과(Centrifugal Effect)는 관절 및 몸체 속도가 증가할수록 더욱 중요해진다. 느린 보행에서는 상대적으로 영향이 작을 수 있지만 달리기, 점프, 빠른 회전 또는 자세 복구 동작(Recovery Maneuver)에서는 필요한 액추에이터 토크에 큰 영향을 줄 수 있다. 동적 제어기(Dynamic Controller)는 이러한 속도 의존 항을 고려함으로써 명령된 움직임이 이상적인 정적 근사가 아니라 실제 다물체 시스템의 결합된 거동을 반영하도록 한다.

지면 접촉(Ground Contact)은 다리형 로봇 동역학을 자유공간 로봇 조작(Free-Space Robotic Manipulation)과 근본적으로 구별하는 요소이다. 각각의 스탠스 발(Stance Foot)은 로봇을 지지하고 가속시키는 지면 반력을 생성하지만, 스윙 발(Swing Foot)은 일반적으로 지지 접촉력을 발생시키지 않는다. 접촉은 반복적으로 생성되고 사라지므로 사족보행 로봇 동역학은 연속적인 다물체 운동과 착지(Touchdown), 이륙(Liftoff), 미끄러짐(Slipping), 충격(Impact)과 같은 이산 사건으로 구성되는 하이브리드 시스템(Hybrid System)이다.

스탠스 접촉(Stance Contact)은 허용 가능한 움직임에 제약을 부여한다. 이상적인 강체 무미끄럼(Rigid No-Slip) 조건에서는 지면에 대한 접촉점의 속도가 거의 0이라고 가정한다. 이러한 조건은 접촉 자코비안과 일반화 속도의 관계를 통해 표현할 수 있다. 접촉 제약(Contact Constraint)을 미분하면 가속도 수준의 관계를 얻을 수 있으며, 이를 역동역학(Inverse Dynamics), 구속 동역학(Constrained Dynamics), 최적화 및 전신 제어에 포함할 수 있다.

지면 반력은 물리적인 접촉 조건을 만족해야 한다. 수직 접촉력(Normal Contact Force)은 로봇을 표면으로부터 밀어낼 수 있지만 지면을 발 방향으로 끌어당길 수는 없다. 접선 방향 힘(Tangential Force)은 사용 가능한 마찰에 의해 제한되며 일반적으로 마찰 원뿔(Friction Cone) 또는 선형화된 마찰 피라미드(Linearized Friction Pyramid)로 표현된다. 명령된 힘이 이러한 한계를 초과하면 발이 미끄러질 수 있으며 가정한 접촉 모델은 더 이상 유효하지 않게 된다.

무게중심(Center of Mass)은 전신 동역학을 설명하기 위한 유용한 전역적 표현을 제공한다. 무게중심의 가속도는 외력의 합에 의해 결정되며 주요 외력은 중력과 지면 반력이다. 내부 관절력(Internal Joint Force)은 외부 환경과의 상호작용 없이는 시스템의 무게중심을 직접 가속할 수 없다. 이러한 원리를 이용하면 복잡한 관절형 동역학을 많은 보행 계획 및 제어 문제에서 보다 단순한 중심 동역학 모델(Centroidal Model)로 축소할 수 있다.

각운동량(Angular Momentum) 역시 로봇이 전체 몸체의 회전 운동을 제어해야 하기 때문에 중요하다. 지면 반력은 힘의 크기와 접촉 위치에 따라 무게중심 주변에 모멘트를 발생시킨다. 다리 움직임 역시 내부 각운동량을 재분배할 수 있다. 따라서 중심 동역학(Centroidal Dynamics)은 무게중심의 병진 운동과 전신 각운동량을 모두 설명하며, 단순화된 템플릿 모델과 전체 강체 동역학 사이를 연결하는 강력한 중간 모델을 제공한다.

전체 다물체 방정식을 모든 계획 단계에서 계산하는 것은 계산 비용이 높을 수 있기 때문에 단순화된 동역학 모델(Simplified Dynamic Model)이 자주 사용된다. 단일 강체 모델(Single Rigid Body Model)은 로봇의 몸체와 전체 질량을 접촉력이 작용하는 하나의 강체로 취급한다. 이 근사는 세부적인 다리 관성을 무시하지만 모델 예측 제어(Model Predictive Control), 발 디딤 계획(Foothold Planning) 및 지면 반력 최적화에서 주요 동역학을 충분히 표현할 수 있는 경우가 많다.

다리 관성, 빠른 다리 운동, 탑재물, 조작(Manipulation) 또는 공격적인 기동(Aggressive Maneuver)의 영향을 무시할 수 없는 경우에는 전신 모델(Full-Body Model)이 중요해진다. 전신 모델은 개별 링크, 관절, 관성 파라미터(Inertial Parameter), 액추에이터 토크 및 접촉 제약을 명시적으로 표현한다. 이를 통해 제어기는 다리 가속도, 몸체 운동, 중력 보상(Gravity Compensation) 및 여러 동시 접촉의 영향을 고려하면서 동역학적으로 일관된 관절 명령을 계산할 수 있다.

역동역학(Inverse Dynamics)은 원하는 가속도를 구현하면서 접촉 제약을 만족하기 위해 필요한 일반화 힘 또는 액추에이터 토크를 계산한다. 사족보행 로봇에서는 부동 베이스를 직접 구동할 수 없기 때문에 이 문제에 추가적인 제약이 존재한다. 몸체 가속도는 스탠스 다리를 통해 전달되는 힘으로 생성해야 한다. 최적화 기반 역동역학(Optimization-Based Inverse Dynamics)은 마찰, 토크 및 접촉 제한을 만족하면서 이러한 힘을 분배할 수 있다.

순동역학(Forward Dynamics)은 이와 반대되는 계산을 수행한다. 현재 구성, 속도, 액추에이터 토크 및 외력이 주어지면 그 결과로 발생하는 일반화 가속도를 계산한다. 순동역학은 적용된 명령에 따라 로봇 상태가 어떻게 변화하는지를 예측하기 때문에 물리 시뮬레이션(Physics Simulation)의 핵심이다. 또한 제어기 검증, 시스템 식별(System Identification), 강화학습(Reinforcement Learning), 궤적 예측 및 외란 응답 평가에도 유용하다.

부동 베이스(Floating Base)는 구동 좌표와 비구동 좌표(Unactuated Coordinate) 사이에 중요한 차이를 만든다. 모터는 6개의 몸체 좌표에 직접 힘이나 토크를 발생시키는 것이 아니라 관절에서만 직접 토크를 생성한다. 몸체는 중력과 외력, 특히 스탠스 접촉을 통해 전달되는 힘에 의해서만 가속될 수 있다. 따라서 몸체의 위치와 방향을 유지하려면 지지하는 발 전체에 적절한 접촉력 분포를 생성하도록 다리 구동을 협조적으로 제어해야 한다.

여러 발이 동시에 로봇을 지지하는 경우 접촉력 분배(Contact-Force Distribution)는 일반적으로 유일하지 않다. 각각의 발에 작용하는 여러 힘의 조합이 몸체에 동일한 목표 합력과 모멘트를 생성할 수 있다. 제어기는 이러한 중복성(Redundancy)을 활용하여 에너지 소비를 최소화하고, 액추에이터 포화(Actuator Saturation)를 방지하며, 마찰 여유를 유지하고, 다리 사이의 하중을 균형 있게 분배하거나 강건성을 향상시킬 수 있다. 최적화는 바람직한 힘 분포를 선택하는 체계적인 방법을 제공한다.

액추에이터 제한(Actuator Limit)은 실현 가능한 동역학에 직접적인 제약을 부여한다. 모터와 전달장치(Transmission)는 제한된 토크, 속도, 출력 및 열적 성능을 갖는다. 어떤 움직임이 운동학적으로 도달 가능하더라도 필요한 관절 토크가 액추에이터의 성능을 초과하면 동역학적으로 실행할 수 없다. 따라서 보행 동작을 설계할 때에는 관절 제한, 접촉 마찰, 배터리 출력, 전달 효율 및 열적 제약과 함께 동역학적 실행 가능성(Dynamic Feasibility)을 평가해야 한다.

충격 동역학(Impact Dynamics)은 발이 지면에 착지할 때 중요해진다. 스윙 발이 비교적 낮은 속도로 지형에 접근하더라도 접촉 순간에는 급격한 속도 변화와 큰 충격력이 발생할 수 있다. 발, 전달장치, 구조 또는 제어기의 컴플라이언스(Compliance)는 충격의 크기를 감소시킬 수 있다. 따라서 정확한 착지 타이밍과 속도 제어는 기계적 응력을 줄이고, 반발을 방지하며, 접지력을 유지하고, 상태 추정(State Estimation)의 일관성을 향상시키는 데 중요하다.

탑재물(Payload)은 전체 질량, 무게중심 위치, 관성 및 필요한 접촉력을 변화시켜 전신 동역학을 수정한다. 몸체 중심보다 높거나 멀리 장착된 탑재물은 회전 모멘트를 크게 증가시키고 안정성 여유를 감소시킬 수 있다. 사족보행 로봇에 장착된 매니퓰레이터(Manipulator)의 움직임은 추가적인 시간 가변 관성 효과(Time-Varying Inertial Effect)를 발생시킨다. 따라서 전신 모델링은 이동 조작(Mobile Manipulation) 및 화물 운송 응용에서 특히 중요하다.

모델 정확도(Model Accuracy)는 관성 및 액추에이터 파라미터의 품질에 따라 달라진다. 링크 질량, 무게중심, 관성 텐서(Inertia Tensor), 관절 마찰, 전달 특성 및 모터 토크 상수는 공칭 컴퓨터 지원 설계(Computer-Aided Design) 값과 실제로 차이가 있을 수 있다. 시스템 식별을 이용하면 측정된 운동, 토크, 전류 및 힘 데이터로부터 이러한 파라미터를 추정할 수 있다. 향상된 파라미터 추정은 예측 정확도를 높이고 모델 기반 제어기(Model-Based Controller)의 체계적인 오차를 감소시킨다.

실제 로봇에는 이상적인 강체 동역학 방정식으로 완전히 표현할 수 없는 동역학도 존재한다. 기어박스 백래시(Gearbox Backlash), 구조적 유연성, 케이블 힘, 액추에이터 지연, 모터 포화, 발 컴플라이언스, 지형 변형 및 모델링되지 않은 마찰은 예측과 실제 관측 사이의 차이를 발생시킬 수 있다. 따라서 완벽한 수학적 정확성에만 의존하기보다 강건 제어(Robust Control), 피드백 보정, 외란 추정(Disturbance Estimation) 및 적응 기법(Adaptive Technique)을 물리 모델과 함께 사용한다.

동역학 모델의 선택은 제어 계층(Control Layer)과 계산 목적에 따라 달라진다. 단순화된 모델은 긴 예측 구간에서 빠른 예측을 수행하는 데 유용하고, 전신 모델은 정확한 단기 제어와 토크 생성에 유용하다. 현대적인 사족보행 로봇 아키텍처에서는 두 접근법을 결합하여 축소 차수 동역학(Reduced-Order Dynamics)을 계획 및 모델 예측 제어에 사용하고, 전신 최적화(Full-Body Optimization) 또는 역동역학을 저수준 실행(Low-Level Execution)에 사용하는 경우가 많다.

전신 동역학 모델(Full-Body Dynamic Model)은 궁극적으로 원하는 보행 동작을 물리적으로 실현 가능한 힘과 토크에 연결한다. 이는 액추에이터 명령이 관절형 다리를 통해 어떻게 전달되는지, 접촉력이 부동 몸체를 어떻게 가속하고 안정화하는지, 그리고 운동 과정에서 관성과 운동량이 어떻게 변화하는지를 설명한다. 따라서 신뢰성 높은 사족보행 로봇 제어는 다물체 동역학(Multibody Dynamics), 접촉 제약, 마찰 모델, 액추에이터 제한, 상태 추정 및 최적화를 하나의 일관된 물리적 프레임워크로 통합하는 것에 기반해야 한다.

##  

## 01.04. Actuator Selection Quasi Direct Drive SEA [w/Code]

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

Actuator selection is one of the most influential design decisions in a quadruped robot because actuators determine achievable joint torque, speed, bandwidth, efficiency, impact tolerance, and force-control quality. Unlike manipulators operating on fixed bases, legged robots repeatedly accelerate their limbs and experience large ground impacts. The actuator must therefore satisfy both locomotion performance and physical interaction requirements.

A quadruped joint actuator typically combines an electric motor, transmission, bearings, position sensing, power electronics, and structural housing. The transmission converts motor speed and torque into joint-level motion appropriate for the leg. Selecting these components cannot be performed independently because motor torque density, reduction ratio, reflected inertia, backlash, efficiency, thermal capacity, and mechanical packaging strongly interact.

Joint requirements should be derived from expected locomotion tasks before choosing a motor or gearbox. Walking, trotting, running, jumping, stair climbing, payload transport, and disturbance recovery produce substantially different torque-speed profiles. Simulation using representative trajectories can estimate continuous torque, peak torque, maximum joint velocity, mechanical power, and energy consumption across the hip and knee joints.

Peak torque determines whether the robot can survive demanding transient events such as acceleration, landing, or recovery, whereas continuous torque is strongly related to thermal capability. Selecting an actuator solely from peak torque can result in overheating during sustained operation. Conversely, designing entirely around continuous torque may create excessive mass. Practical selection therefore considers torque-duration characteristics and realistic duty cycles.

Mechanical power is approximately the product of joint torque and angular velocity. High-performance locomotion may require high torque and high velocity simultaneously, making power density as important as torque density. The actuator must operate across the required torque-speed envelope rather than satisfy only a single maximum value. Motor voltage, winding characteristics, inverter current, transmission ratio, and battery voltage all influence this envelope.

Traditional highly geared actuators use large reduction ratios to amplify motor torque. This approach allows relatively small motors to generate large output torque, but high reduction ratios increase reflected motor inertia, friction, backlash, and resistance to externally imposed motion. These characteristics can reduce force-control quality and impact tolerance, which are particularly important when robot feet repeatedly interact with uncertain terrain.

Backdrivability describes how easily external forces applied at the joint output can cause motion through the transmission and motor. High backdrivability allows the leg to respond naturally to terrain impacts and enables joint torque to be inferred more directly from motor current. Low-backdrivability transmissions can mechanically resist disturbances, but they may isolate the motor from useful contact information and produce less transparent physical interaction.

Quasi-direct drive, commonly abbreviated QDD, addresses these issues by combining a high-torque-density motor with a relatively low transmission ratio. Instead of relying on a small high-speed motor and large gear reduction, QDD uses a larger motor capable of producing substantial torque before reduction. Typical design objectives include low reflected inertia, high backdrivability, high control bandwidth, efficient torque transmission, and robust impact response.

The reflected motor inertia observed at the joint increases approximately with the square of the transmission ratio. Consequently, even a moderate increase in reduction ratio can substantially increase apparent output inertia. Low-ratio QDD architectures reduce this effect, allowing the joint to respond more freely to external disturbances. This property is highly beneficial for dynamic locomotion where feet frequently collide with the ground.

QDD actuators are particularly compatible with torque control. When transmission friction and reduction ratio are relatively low, motor current can provide a useful estimate of output torque because electromagnetic motor torque is approximately proportional to current. High-quality current control can therefore support joint torque control without requiring complex high-ratio transmission models, although dedicated torque sensing may still improve accuracy.

Large-diameter brushless permanent-magnet motors are commonly associated with QDD because increasing motor radius can significantly improve torque production. Outrunner or specialized frameless motors may provide high torque density at moderate rotational speed. However, larger motors increase joint dimensions and can complicate leg packaging. Designers must balance electromagnetic performance against limb inertia, structural integration, cooling, and available space.

Transmission options for QDD include low-ratio planetary gears, cycloidal mechanisms, belts, and other compact reductions. Planetary gearboxes provide high torque density and coaxial packaging, while belt drives can offer low backlash and mechanical simplicity. Each transmission introduces different efficiency, stiffness, backlash, shock resistance, bearing-load capability, and manufacturing requirements that must be evaluated at the complete actuator level.

Series elastic actuators, abbreviated SEA, introduce a deliberately compliant elastic element between the motor-transmission system and the output load. By measuring deformation of this elastic element, joint force or torque can be estimated using its known stiffness. This architecture converts mechanical compliance into both an impact-management mechanism and a sensing element, making SEA attractive for controlled physical interaction.

The spring in an SEA stores and releases mechanical energy while filtering high-frequency impacts transmitted between the environment and drivetrain. This can protect gears and motors during touchdown and collisions. Compliance can also improve force-control stability when interacting with uncertain terrain. However, the spring introduces an additional dynamic state and reduces the direct mechanical stiffness between the commanded motor position and joint output.

SEA torque measurement can be expressed conceptually as τ = kΔθ for a rotational elastic element, where k represents spring stiffness and Δθ represents measured elastic deflection. Accurate torque estimation therefore requires reliable measurement of relative displacement across the spring and sufficiently well-characterized stiffness. Sensor resolution, hysteresis, temperature dependence, mechanical tolerances, and nonlinear spring behavior can affect estimation quality.

Spring stiffness represents a central SEA design trade-off. A stiff spring provides high mechanical bandwidth and small output deflection but generates small measurable deformation for a given torque. A softer spring improves force-sensing resolution and impact absorption but can reduce position-control bandwidth and allow large deflections. The appropriate stiffness depends on expected contact forces, locomotion frequency, control architecture, and mechanical travel limits.

QDD and SEA should not be interpreted as mutually exclusive philosophies. QDD primarily reduces transmission impedance through low gear reduction and low reflected inertia, whereas SEA intentionally introduces measurable compliance. Hybrid actuators can combine relatively low-ratio transmissions with elastic elements to achieve both backdrivability and controlled compliance. The appropriate architecture depends on the desired balance between transparency, force sensing, bandwidth, and robustness.

For highly dynamic quadrupeds, low limb inertia is a major requirement. Heavy actuators mounted near the knee or lower leg increase the energy required for swing motion and generate larger reaction forces on the trunk. Designers therefore attempt to position heavy motors proximally near the body when possible. Mechanical linkages, belts, or remote transmissions may transfer power toward distal joints while keeping major actuator mass close to the trunk.

Actuator bandwidth determines how rapidly commanded torque or motion can be produced. High-bandwidth torque control enables the robot to regulate ground reaction forces, reject disturbances, and execute dynamic gaits. Bandwidth is affected by motor electrical dynamics, current-loop performance, transmission compliance, structural flexibility, sensing delay, communication latency, and control frequency. Mechanical actuator specifications alone therefore do not determine achievable control performance.

Thermal management often establishes the practical continuous-performance limit. Copper losses increase approximately with the square of motor current, while iron losses and inverter losses add further heat. Compact sealed quadruped joints have limited cooling area and may operate in environments where fans are undesirable. Temperature sensors, thermal models, conductive housings, heat paths, and current derating strategies are therefore essential parts of actuator design.

Regenerative operation also influences actuator and power-system selection. During deceleration, landing, or lowering of the body, motors can operate as generators and return energy toward the electrical bus. The inverter and battery must safely absorb this energy. If regenerative power exceeds battery acceptance limits, bus voltage can rise rapidly, requiring braking resistors, energy-management logic, or alternative protective mechanisms.

Position and velocity sensing are required even when torque control is the primary objective. High-resolution encoders support commutation, joint-state estimation, trajectory tracking, and disturbance observation. QDD systems may estimate torque primarily from current, while SEA systems generally require additional measurement across the elastic element. Sensor architecture should therefore be designed together with the mechanical transmission and control strategy.

Joint bearings must withstand loads that can greatly exceed nominal actuator torque requirements. Ground impacts generate radial, axial, and moment loads through the leg structure, and the gearbox itself should not necessarily carry all structural loads. Dedicated output bearings can separate structural loading from transmission components. Bearing arrangement, shaft stiffness, housing deformation, and gear alignment consequently influence actuator durability and control precision.

Actuator selection should include fault and overload behavior. A quadruped may encounter unexpected foot impacts, falls, blocked joints, or actuator saturation. Current limiting, mechanical stops, thermal protection, compliant elements, shock-resistant transmissions, and software torque limits can prevent temporary disturbances from becoming permanent damage. The desired failure mode should be considered during design rather than added only after hardware testing.

Efficiency has direct consequences for robot endurance because locomotion repeatedly transfers energy through every leg joint. Electrical and mechanical losses reduce battery operating time and generate heat that must be removed. QDD can provide high efficiency by avoiding large transmission losses, but its larger motors may require significant current. SEA can recover some elastic energy during cyclic motion, although actual benefits depend strongly on gait and spring tuning.

No actuator architecture is universally optimal for every quadruped. QDD is attractive for highly dynamic robots requiring backdrivability, torque transparency, and rapid response, while SEA is attractive when force sensing, impact isolation, and compliant interaction are dominant requirements. Higher-ratio geared actuators may remain appropriate for slower robots requiring high static torque, compact dimensions, or strong load-holding capability.

The final actuator should therefore be selected at the system level rather than from isolated motor specifications. Required torque-speed envelopes, limb inertia, transmission ratio, reflected inertia, force sensing, compliance, efficiency, thermal limits, battery capability, impact loading, packaging, reliability, and control bandwidth must be evaluated together. Successful quadruped design treats the actuator as an integrated electromechanical and control subsystem that fundamentally shapes locomotion behavior.

액추에이터 선정(Actuator Selection)은 사족보행 로봇(Quadruped Robot)에서 가장 중요한 설계 결정 중 하나이다. 액추에이터는 구현 가능한 관절 토크(Joint Torque), 속도, 대역폭(Bandwidth), 효율, 충격 내성(Impact Tolerance), 힘 제어 품질(Force-Control Quality)을 결정하기 때문이다. 고정 베이스에서 동작하는 매니퓰레이터(Manipulator)와 달리 다리형 로봇은 다리를 반복적으로 가속하고 큰 지면 충격을 받는다. 따라서 액추에이터는 보행 성능과 물리적 상호작용 요구조건을 모두 만족해야 한다.

사족보행 로봇의 관절 액추에이터(Joint Actuator)는 일반적으로 전기 모터, 전달장치(Transmission), 베어링, 위치 센서(Position Sensor), 전력전자 장치(Power Electronics), 구조 하우징(Structural Housing)을 결합하여 구성한다. 전달장치는 모터의 속도와 토크를 다리 관절에 적합한 운동으로 변환한다. 모터 토크 밀도(Torque Density), 감속비(Reduction Ratio), 반사 관성(Reflected Inertia), 백래시(Backlash), 효율, 열용량 및 기계적 패키징이 서로 강하게 연관되므로 이러한 구성요소를 독립적으로 선정해서는 안 된다.

모터나 기어박스를 선정하기 전에 예상되는 보행 임무로부터 관절 요구조건(Joint Requirement)을 도출해야 한다. 걷기, 트로팅(Trotting), 달리기, 점프, 계단 등반, 탑재물 운송 및 외란 복구(Disturbance Recovery)는 서로 상당히 다른 토크-속도 프로파일(Torque-Speed Profile)을 발생시킨다. 대표적인 궤적을 이용한 시뮬레이션을 통해 고관절과 무릎 관절에서 요구되는 연속 토크, 최대 토크, 최대 관절 속도, 기계적 출력 및 에너지 소비를 추정할 수 있다.

최대 토크(Peak Torque)는 가속, 착지 또는 자세 복구와 같은 높은 과도 부하(Transient Load)를 로봇이 견딜 수 있는지를 결정하는 반면, 연속 토크(Continuous Torque)는 열적 성능과 밀접하게 관련된다. 최대 토크만을 기준으로 액추에이터를 선정하면 지속적인 운용 과정에서 과열될 수 있다. 반대로 연속 토크만을 기준으로 설계하면 불필요하게 질량이 증가할 수 있다. 따라서 실제 액추에이터 선정에서는 토크 지속시간 특성과 현실적인 듀티 사이클(Duty Cycle)을 함께 고려해야 한다.

기계적 출력(Mechanical Power)은 대략적으로 관절 토크와 각속도의 곱으로 표현된다. 고성능 보행에서는 높은 토크와 높은 속도가 동시에 요구될 수 있기 때문에 토크 밀도뿐만 아니라 출력 밀도(Power Density)도 중요하다. 액추에이터는 단일 최대값만 만족하는 것이 아니라 요구되는 전체 토크-속도 영역(Torque-Speed Envelope)에서 동작할 수 있어야 한다. 모터 전압, 권선 특성, 인버터 전류, 감속비 및 배터리 전압은 모두 이러한 동작 영역에 영향을 미친다.

전통적인 고감속 액추에이터(Highly Geared Actuator)는 큰 감속비를 사용하여 모터 토크를 증폭한다. 이 방식은 상대적으로 작은 모터로 큰 출력 토크를 생성할 수 있지만 높은 감속비는 반사 모터 관성, 마찰, 백래시 및 외부 힘에 의해 움직이는 것에 대한 저항을 증가시킨다. 이러한 특성은 로봇의 발이 불확실한 지형과 반복적으로 상호작용할 때 특히 중요한 힘 제어 품질과 충격 내성을 저하시킬 수 있다.

역구동성(Backdrivability)은 관절 출력부에 작용하는 외력이 전달장치와 모터를 역방향으로 얼마나 쉽게 움직일 수 있는지를 나타낸다. 높은 역구동성은 다리가 지형 충격에 자연스럽게 반응하도록 하며 모터 전류로부터 관절 토크를 보다 직접적으로 추정할 수 있도록 한다. 역구동성이 낮은 전달장치는 외란에 기계적으로 저항할 수 있지만 모터를 유용한 접촉 정보로부터 분리하고 물리적 상호작용의 투명성(Transparency)을 저하시킬 수 있다.

준직접 구동(Quasi-Direct Drive, QDD)은 높은 토크 밀도를 갖는 모터와 상대적으로 낮은 감속비를 결합하여 이러한 문제를 해결한다. 작은 고속 모터와 큰 기어 감속에 의존하는 대신 준직접 구동은 감속 이전부터 상당한 토크를 발생시킬 수 있는 더 큰 모터를 사용한다. 대표적인 설계 목표에는 낮은 반사 관성, 높은 역구동성, 높은 제어 대역폭, 효율적인 토크 전달 및 강건한 충격 응답이 포함된다.

관절에서 관측되는 반사 모터 관성(Reflected Motor Inertia)은 대략적으로 전달장치 감속비의 제곱에 비례하여 증가한다. 따라서 감속비가 비교적 조금만 증가해도 관절 출력단에서 느껴지는 관성이 크게 증가할 수 있다. 저감속비 준직접 구동 구조는 이러한 효과를 감소시켜 관절이 외부 외란에 보다 자유롭게 반응하도록 한다. 이러한 특성은 발이 지면과 빈번하게 충돌하는 동적 보행(Dynamic Locomotion)에서 매우 유리하다.

준직접 구동 액추에이터는 특히 토크 제어(Torque Control)에 적합하다. 전달 마찰과 감속비가 비교적 낮으면 전자기적 모터 토크가 전류에 대략 비례하므로 모터 전류를 이용하여 출력 토크를 유용하게 추정할 수 있다. 따라서 고품질 전류 제어(Current Control)를 이용하면 복잡한 고감속 전달 모델 없이도 관절 토크 제어를 구현할 수 있다. 다만 전용 토크 센싱(Dedicated Torque Sensing)을 적용하면 정확도를 더욱 향상시킬 수 있다.

대구경 브러시리스 영구자석 모터(Large-Diameter Brushless Permanent-Magnet Motor)는 모터 반경을 증가시키면 토크 생성 능력을 크게 향상시킬 수 있기 때문에 준직접 구동 구조에서 흔히 사용된다. 아우트러너 모터(Outrunner Motor) 또는 특수 프레임리스 모터(Frameless Motor)는 중간 수준의 회전 속도에서 높은 토크 밀도를 제공할 수 있다. 그러나 큰 모터는 관절 크기를 증가시키고 다리 패키징을 어렵게 만들 수 있으므로 전자기적 성능과 다리 관성, 구조 통합, 냉각 및 사용 가능한 공간 사이의 균형을 고려해야 한다.

준직접 구동을 위한 전달장치에는 저감속비 유성기어(Planetary Gear), 사이클로이드 메커니즘(Cycloidal Mechanism), 벨트 및 기타 소형 감속장치를 사용할 수 있다. 유성기어박스는 높은 토크 밀도와 동축 패키징(Coaxial Packaging)을 제공하며, 벨트 구동은 낮은 백래시와 기계적 단순성을 제공할 수 있다. 각 전달 방식은 서로 다른 효율, 강성, 백래시, 충격 저항성, 베어링 하중 능력 및 제조 요구조건을 가지므로 전체 액추에이터 수준에서 평가해야 한다.

직렬 탄성 액추에이터(Series Elastic Actuator, SEA)는 모터-전달 시스템과 출력 부하 사이에 의도적으로 유연한 탄성 요소(Elastic Element)를 배치한다. 이 탄성 요소의 변형을 측정하고 알려진 강성을 이용하면 관절 힘 또는 토크를 추정할 수 있다. 이러한 구조는 기계적 컴플라이언스(Compliance)를 충격 관리 메커니즘과 센싱 요소로 동시에 활용하므로 제어된 물리적 상호작용에 적합하다.

직렬 탄성 액추에이터의 스프링은 환경과 구동계 사이에서 전달되는 고주파 충격을 필터링하면서 기계적 에너지를 저장하고 방출한다. 이를 통해 착지나 충돌 시 기어와 모터를 보호할 수 있다. 또한 컴플라이언스는 불확실한 지형과 상호작용할 때 힘 제어 안정성을 향상시킬 수 있다. 그러나 스프링은 추가적인 동적 상태(Dynamic State)를 도입하고 명령된 모터 위치와 관절 출력 사이의 직접적인 기계적 강성을 감소시킨다.

직렬 탄성 액추에이터의 토크 측정은 회전 탄성 요소에 대해 개념적으로 τ = kΔθ로 표현할 수 있다. 여기에서 k는 스프링 강성(Spring Stiffness), Δθ는 측정된 탄성 변형을 나타낸다. 따라서 정확한 토크 추정을 위해서는 스프링 양단의 상대 변위를 신뢰성 있게 측정하고 강성 특성을 충분히 정확하게 파악해야 한다. 센서 분해능, 히스테리시스(Hysteresis), 온도 의존성, 기계적 공차 및 비선형 스프링 특성은 추정 정확도에 영향을 줄 수 있다.

스프링 강성은 직렬 탄성 액추에이터 설계에서 핵심적인 절충 요소이다. 강한 스프링은 높은 기계적 대역폭과 작은 출력 변형을 제공하지만 동일한 토크에 대해 측정 가능한 변형량이 작다. 반대로 부드러운 스프링은 힘 센싱 분해능과 충격 흡수 능력을 향상시키지만 위치 제어 대역폭을 감소시키고 큰 변형을 발생시킬 수 있다. 적절한 강성은 예상 접촉력, 보행 주파수, 제어 아키텍처 및 기계적 이동 한계에 따라 결정된다.

준직접 구동과 직렬 탄성 액추에이터를 서로 배타적인 설계 철학으로 이해해서는 안 된다. 준직접 구동은 주로 낮은 기어 감속비와 낮은 반사 관성을 통해 전달 임피던스(Transmission Impedance)를 감소시키는 반면, 직렬 탄성 액추에이터는 의도적으로 측정 가능한 컴플라이언스를 도입한다. 하이브리드 액추에이터(Hybrid Actuator)는 비교적 낮은 감속비 전달장치와 탄성 요소를 결합하여 역구동성과 제어된 컴플라이언스를 동시에 구현할 수 있다.

고도의 동적 사족보행 로봇에서는 낮은 다리 관성(Limb Inertia)이 중요한 요구조건이다. 무거운 액추에이터를 무릎이나 하부 다리에 배치하면 스윙 운동에 필요한 에너지가 증가하고 몸체에 더 큰 반력을 발생시킨다. 따라서 설계자는 가능한 경우 무거운 모터를 몸체에 가까운 근위부(Proximal Region)에 배치하려고 한다. 기계적 링크, 벨트 또는 원격 전달장치를 사용하면 주요 액추에이터 질량을 몸체 근처에 유지하면서 말단 관절로 동력을 전달할 수 있다.

액추에이터 대역폭(Actuator Bandwidth)은 명령된 토크나 움직임을 얼마나 빠르게 생성할 수 있는지를 결정한다. 높은 대역폭의 토크 제어는 로봇이 지면 반력을 조절하고 외란을 억제하며 동적 보행 패턴을 실행할 수 있도록 한다. 대역폭은 모터 전기 동역학, 전류 루프(Current Loop) 성능, 전달장치 컴플라이언스, 구조적 유연성, 센싱 지연, 통신 지연 및 제어 주파수의 영향을 받는다. 따라서 기계적 액추에이터 사양만으로 실제 제어 성능을 결정할 수는 없다.

열관리(Thermal Management)는 실제 연속 운용 성능의 한계를 결정하는 경우가 많다. 구리 손실(Copper Loss)은 대략적으로 모터 전류의 제곱에 비례하여 증가하며 철손(Iron Loss)과 인버터 손실이 추가적인 열을 발생시킨다. 소형 밀폐형 사족보행 로봇 관절은 냉각 면적이 제한적이며 팬을 사용하기 어려운 환경에서 운용될 수도 있다. 따라서 온도 센서, 열 모델(Thermal Model), 열전도 하우징, 방열 경로 및 전류 디레이팅(Current Derating) 전략은 액추에이터 설계의 필수적인 요소이다.

회생 동작(Regenerative Operation) 역시 액추에이터와 전력 시스템 선정에 영향을 준다. 감속, 착지 또는 몸체를 낮추는 과정에서 모터는 발전기로 동작하여 전기 에너지를 전원 버스로 반환할 수 있다. 인버터와 배터리는 이러한 에너지를 안전하게 흡수할 수 있어야 한다. 회생 전력이 배터리의 수용 한계를 초과하면 버스 전압이 빠르게 상승할 수 있으므로 제동 저항(Braking Resistor), 에너지 관리 로직 또는 다른 보호 메커니즘이 필요하다.

토크 제어가 주요 목적이더라도 위치 및 속도 센싱(Position and Velocity Sensing)은 필요하다. 고해상도 인코더(High-Resolution Encoder)는 정류(Commutation), 관절 상태 추정, 궤적 추종 및 외란 관측을 지원한다. 준직접 구동 시스템에서는 주로 전류를 통해 토크를 추정할 수 있지만, 직렬 탄성 액추에이터 시스템에서는 일반적으로 탄성 요소 양단의 추가적인 변위 측정이 필요하다. 따라서 센서 아키텍처는 기계적 전달장치 및 제어 전략과 함께 설계해야 한다.

관절 베어링(Joint Bearing)은 공칭 액추에이터 토크 요구조건보다 훨씬 큰 하중을 견뎌야 할 수 있다. 지면 충격은 다리 구조를 통해 반경 방향 하중, 축 방향 하중 및 모멘트 하중을 발생시키며 기어박스 자체가 이러한 모든 구조적 하중을 담당하도록 설계할 필요는 없다. 전용 출력 베어링(Output Bearing)을 사용하면 구조 하중을 전달 구성요소로부터 분리할 수 있다. 따라서 베어링 배치, 축 강성, 하우징 변형 및 기어 정렬은 액추에이터 내구성과 제어 정밀도에 영향을 준다.

액추에이터 선정에는 고장 및 과부하 거동(Fault and Overload Behavior)도 포함되어야 한다. 사족보행 로봇은 예상하지 못한 발 충격, 넘어짐, 관절 구속 또는 액추에이터 포화를 경험할 수 있다. 전류 제한, 기계적 스토퍼(Mechanical Stop), 열 보호, 탄성 요소, 충격 저항성 전달장치 및 소프트웨어 토크 제한을 통해 일시적인 외란이 영구적인 손상으로 이어지는 것을 방지할 수 있다. 원하는 고장 모드(Failure Mode)는 하드웨어 시험 이후에 추가하는 것이 아니라 설계 단계에서부터 고려해야 한다.

효율(Efficiency)은 보행 과정에서 모든 다리 관절을 통해 에너지가 반복적으로 전달되므로 로봇의 운용시간에 직접적인 영향을 미친다. 전기적 및 기계적 손실은 배터리 운용시간을 감소시키고 제거해야 하는 열을 발생시킨다. 준직접 구동은 큰 전달 손실을 방지함으로써 높은 효율을 제공할 수 있지만 큰 모터는 상당한 전류를 요구할 수 있다. 직렬 탄성 액추에이터는 반복적인 운동에서 일부 탄성 에너지를 회수할 수 있지만 실제 효과는 보행 패턴과 스프링 튜닝에 크게 의존한다.

모든 사족보행 로봇에 보편적으로 최적인 액추에이터 구조는 존재하지 않는다. 준직접 구동은 높은 역구동성, 토크 투명성(Torque Transparency) 및 빠른 응답을 요구하는 고동적 로봇에 적합하며, 직렬 탄성 액추에이터는 힘 센싱, 충격 절연(Impact Isolation) 및 유연한 상호작용이 주요 요구조건일 때 유리하다. 높은 감속비의 기어 액추에이터는 높은 정적 토크, 작은 크기 또는 강한 하중 유지 능력을 요구하는 저속 로봇에서는 여전히 적합할 수 있다.

따라서 최종 액추에이터는 개별적인 모터 사양이 아니라 시스템 수준(System Level)에서 선정해야 한다. 요구되는 토크-속도 영역, 다리 관성, 감속비, 반사 관성, 힘 센싱, 컴플라이언스, 효율, 열적 한계, 배터리 성능, 충격 하중, 패키징, 신뢰성 및 제어 대역폭을 통합적으로 평가해야 한다. 성공적인 사족보행 로봇 설계에서는 액추에이터를 보행 거동을 근본적으로 결정하는 통합 전기기계 및 제어 하위 시스템(Integrated Electromechanical and Control Subsystem)으로 다루어야 한다.

##  

## 01.05. Quadruped SW Architecture Layered Overview

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Quadruped robot software architecture organizes sensing, estimation, planning, locomotion, control, hardware communication, and safety into coordinated computational layers. Unlike conventional mobile robots, quadrupeds must continuously regulate unstable multibody dynamics while contacts appear and disappear. The architecture must therefore combine deterministic real-time control with higher-level perception, planning, and autonomous decision making.

A layered architecture separates functions according to abstraction, timing requirements, and hardware dependency. Lower layers interact directly with motors, encoders, inertial sensors, and communication buses, while higher layers reason about body motion, terrain, navigation, and missions. Clear interfaces between layers reduce software coupling and allow individual algorithms or hardware components to be replaced without redesigning the complete system.

At the lowest level, device drivers provide access to actuators and sensors. Motor controllers receive current, torque, velocity, or position commands and return encoder positions, velocities, currents, temperatures, and diagnostic information. Drivers for inertial measurement units, force sensors, cameras, LiDAR, and other devices convert hardware-specific protocols into standardized software representations suitable for upper layers.

The hardware abstraction layer isolates control software from specific devices and communication technologies. It defines consistent interfaces for joint commands, joint states, sensor measurements, timing information, and diagnostics. A controller can therefore operate with real hardware, a simulator, or alternative actuator electronics through the same logical interface. This abstraction significantly improves portability, testing, and long-term maintainability.

Real-time execution is essential in the low-level control stack. Joint servo loops may execute at hundreds or thousands of hertz, and timing jitter can directly degrade torque regulation and stability. These loops commonly perform current control, torque control, actuator compensation, limit enforcement, and communication supervision. Their computational path should remain deterministic and should avoid unpredictable operations that could interrupt control timing.

Above actuator control, the state-estimation layer reconstructs the robot state from multiple sensor streams. Joint encoders provide leg configuration, the inertial measurement unit provides angular velocity and acceleration, and contact-related measurements indicate interactions with the terrain. Estimation algorithms combine these observations to determine body orientation, velocity, position, joint state, contact state, and uncertainty required by locomotion controllers.

Contact estimation is particularly important because many control algorithms depend on knowing which feet are supporting the robot. A commanded stance state does not guarantee actual contact, especially on irregular terrain. Contact estimators may use foot force, motor torque, joint motion, inertial measurements, and planned gait phase. Reliable contact information supports state estimation, slip detection, gait transitions, and ground reaction force control.

The robot model layer provides shared descriptions of kinematics, dynamics, joint limits, inertial properties, collision geometry, and actuator capabilities. Forward kinematics, inverse kinematics, Jacobians, rigid-body dynamics, and coordinate transformations should use consistent model parameters. Maintaining a common model prevents subtle discrepancies between estimation, planning, simulation, and control modules that could otherwise produce incompatible assumptions.

The locomotion control layer transforms desired body and foot behavior into dynamically feasible actuator commands. Depending on the architecture, this layer may contain model predictive control, whole-body control, inverse dynamics, impedance control, or learned policies. It regulates body orientation, center-of-mass behavior, foot trajectories, contact forces, and joint motion while respecting physical constraints imposed by the robot and environment.

A gait-management layer determines the temporal pattern of stance and swing phases across the four legs. Walking, trotting, pacing, bounding, and other gaits can be represented through contact schedules, phase variables, duty factors, and transition rules. The gait manager provides future contact information to trajectory generators and predictive controllers while coordinating smooth transitions between locomotion modes.

Foot trajectory generation converts gait timing and foothold targets into continuous swing-leg motion. The trajectory must lift the foot sufficiently to avoid terrain, move it toward the desired contact location, and approach the ground with appropriate velocity. It must also remain within joint workspace and velocity limits. Feedback corrections may modify the nominal trajectory in response to body velocity errors or unexpected terrain interactions.

Foothold planning operates above basic trajectory generation by selecting suitable future contact locations. On flat terrain, footholds can be generated primarily from desired velocity and gait geometry. On rough terrain, the planner must incorporate elevation, slope, obstacle, surface quality, reachability, and stability information. Selected footholds become critical interfaces between terrain perception and the dynamic locomotion controller.

The perception layer processes exteroceptive sensors such as cameras, depth cameras, LiDAR, radar, or specialized ranging devices. It estimates environmental geometry and identifies terrain characteristics relevant to locomotion. Depending on the application, perception may generate point clouds, elevation maps, traversability maps, semantic labels, obstacles, stairs, edges, or candidate support surfaces for subsequent planning modules.

Terrain representation connects perception with locomotion planning. Raw sensor measurements are generally too large and noisy for direct use by high-frequency controllers, so they are converted into compact representations such as local elevation maps or traversability grids. These representations must be updated as the robot moves while maintaining consistent coordinates and uncertainty estimates. Terrain information can then guide foothold selection and body trajectory planning.

The local motion-planning layer determines how the robot should move through its nearby environment. It converts navigation goals into desired body velocity, heading, posture, or short-horizon trajectories while considering obstacles and terrain. For legged robots, local planning may also account for body clearance, slope limits, stepping capability, and feasible contact regions rather than treating the platform as a simple planar mobile base.

Global navigation operates at a longer spatial and temporal horizon. It uses maps, localization, mission goals, and environmental constraints to determine routes through the environment. The resulting route is passed to local planning, which adapts it to current terrain and robot state. This separation allows global reasoning to remain relatively slow while local planning and locomotion respond rapidly to immediate disturbances and newly observed obstacles.

Behavior and mission layers coordinate higher-level tasks such as navigating to inspection points, following an operator, entering designated areas, performing sensing actions, or returning to a charging station. State machines, behavior trees, task planners, or policy-based systems may be used. These layers should issue goals and constraints rather than directly commanding individual joints, preserving separation between mission logic and physical control.

Communication between layers can use shared memory, message passing, publish-subscribe middleware, or direct real-time interfaces depending on latency requirements. High-frequency torque and state data should follow low-latency deterministic paths, whereas maps, mission commands, and diagnostics can tolerate slower asynchronous communication. Selecting communication mechanisms according to timing criticality prevents high-level software activity from disturbing locomotion control.

Time synchronization is essential because quadruped control combines measurements generated by many sensors and processors. Encoder states, inertial measurements, force data, camera frames, and LiDAR scans must correspond to known acquisition times. Timestamp errors can appear as false motion and degrade sensor fusion. Hardware clocks, synchronized timestamps, buffering, and interpolation are therefore important architectural components rather than merely logging conveniences.

The safety layer should span the entire architecture rather than exist as a single high-level module. Low-level protection monitors joint limits, current, voltage, temperature, communication loss, and actuator faults. Higher-level supervision monitors body orientation, fall conditions, localization quality, terrain hazards, and planner failures. Safety responses may include torque limiting, controlled stopping, posture recovery, motor shutdown, or transition to a predefined safe state.

Fault management requires software to distinguish recoverable disturbances from failures requiring shutdown. Temporary foot slip, delayed perception, or a missed step may be handled through feedback and replanning, whereas actuator overheating or communication loss may require degraded operation or emergency stopping. Diagnostic information should propagate upward so that behavior logic understands system capability instead of continuing to request impossible actions.

Simulation should reproduce the same interfaces used by the physical robot whenever possible. A controller developed against a common hardware abstraction can operate in physics simulation and later on real hardware with minimal structural changes. Simulation enables repeatable testing of locomotion, disturbances, terrain, actuator limits, and failure conditions that may be expensive or dangerous to reproduce physically.

Logging and observability are fundamental for developing complex legged systems. Important states, commands, sensor measurements, contact estimates, planner outputs, timing information, and fault events should be recorded with synchronized timestamps. Visualization and replay tools allow engineers to reconstruct failures and compare expected and actual behavior. Without systematic observability, debugging intermittent dynamic instability becomes extremely difficult.

Configuration management ensures that software modules operate with consistent parameters. Robot dimensions, masses, joint limits, controller gains, sensor calibrations, gait parameters, and safety thresholds should be versioned and associated with specific hardware configurations. Uncontrolled parameter duplication across modules can produce subtle errors. A centralized or clearly governed configuration system therefore forms an important part of the software architecture.

Machine-learning components can be integrated at several layers without replacing the complete architecture. Learned estimators may infer contact or terrain properties, learned locomotion policies may generate joint or foot commands, and semantic models may support navigation. However, their inputs, outputs, execution rates, failure handling, and physical constraints should remain clearly defined so they can coexist with deterministic estimation, control, and safety functions.

Computational deployment often spans multiple processors. Motor controllers or microcontrollers handle hard real-time actuator loops, while onboard CPUs execute estimation, planning, and system management. GPUs or accelerators may process perception and learned policies. The software architecture must therefore consider processor boundaries, communication latency, data ownership, synchronization, resource contention, and graceful behavior when individual computing components become unavailable.

A successful quadruped software architecture is ultimately defined not by the number of modules but by the clarity of responsibilities and interfaces between them. Hardware abstraction, state estimation, modeling, gait generation, locomotion control, perception, planning, navigation, mission logic, safety, simulation, and diagnostics must operate at appropriate time scales while sharing consistent robot and environment state.

The layered approach provides a practical framework for managing this complexity while preserving real-time performance and system extensibility. Fast inner loops maintain physical stability, intermediate layers coordinate contacts and locomotion, and slower layers interpret terrain and mission objectives. By connecting these layers through explicit interfaces and synchronized state information, the quadruped can transform high-level intent into safe, dynamically feasible physical behavior.

사족보행 로봇 소프트웨어 아키텍처(Quadruped Robot Software Architecture)는 센싱(Sensing), 상태 추정(Estimation), 계획(Planning), 보행(Locomotion), 제어(Control), 하드웨어 통신(Hardware Communication), 안전(Safety)을 서로 협조하는 계산 계층으로 구성한다. 일반적인 이동 로봇과 달리 사족보행 로봇은 접촉이 생성되고 사라지는 동안 불안정한 다물체 동역학(Multibody Dynamics)을 지속적으로 제어해야 한다. 따라서 아키텍처는 결정론적 실시간 제어(Deterministic Real-Time Control)와 상위 수준의 인식, 계획 및 자율 의사결정을 결합해야 한다.

계층형 아키텍처(Layered Architecture)는 추상화 수준, 시간 요구조건 및 하드웨어 의존성에 따라 기능을 분리한다. 하위 계층은 모터, 인코더, 관성 센서 및 통신 버스와 직접 상호작용하고, 상위 계층은 몸체 운동, 지형, 내비게이션 및 임무를 다룬다. 계층 사이에 명확한 인터페이스를 정의하면 소프트웨어 결합도(Software Coupling)를 줄이고 전체 시스템을 다시 설계하지 않고도 개별 알고리즘이나 하드웨어 구성요소를 교체할 수 있다.

가장 낮은 수준에서는 장치 드라이버(Device Driver)가 액추에이터(Actuator)와 센서에 대한 접근 기능을 제공한다. 모터 제어기는 전류, 토크, 속도 또는 위치 명령을 수신하고 인코더 위치, 속도, 전류, 온도 및 진단 정보를 반환한다. 관성측정장치(Inertial Measurement Unit), 힘 센서, 카메라, 라이다(LiDAR) 및 기타 장치를 위한 드라이버는 하드웨어별 프로토콜을 상위 계층에서 사용할 수 있는 표준화된 소프트웨어 표현으로 변환한다.

하드웨어 추상화 계층(Hardware Abstraction Layer)은 제어 소프트웨어를 특정 장치와 통신 기술로부터 분리한다. 이 계층은 관절 명령, 관절 상태, 센서 측정값, 시간 정보 및 진단 정보를 위한 일관된 인터페이스를 정의한다. 따라서 제어기는 동일한 논리적 인터페이스를 통해 실제 하드웨어, 시뮬레이터 또는 다른 액추에이터 전자장치와 동작할 수 있다. 이러한 추상화는 이식성(Portability), 시험 및 장기적인 유지보수성을 크게 향상시킨다.

저수준 제어 스택(Low-Level Control Stack)에서는 실시간 실행(Real-Time Execution)이 필수적이다. 관절 서보 루프(Joint Servo Loop)는 수백에서 수천 헤르츠로 실행될 수 있으며 타이밍 지터(Timing Jitter)는 토크 제어와 안정성을 직접적으로 저하시킬 수 있다. 이러한 루프에서는 일반적으로 전류 제어, 토크 제어, 액추에이터 보상, 제한조건 적용 및 통신 감시를 수행한다. 계산 경로는 결정론적으로 유지되어야 하며 제어 타이밍을 방해할 수 있는 예측 불가능한 연산을 피해야 한다.

액추에이터 제어 상위에는 여러 센서 스트림으로부터 로봇 상태를 복원하는 상태 추정 계층(State-Estimation Layer)이 존재한다. 관절 인코더는 다리 구성을 제공하고, 관성측정장치는 각속도와 가속도를 제공하며, 접촉 관련 측정값은 지형과의 상호작용을 나타낸다. 상태 추정 알고리즘은 이러한 관측값을 결합하여 보행 제어기에 필요한 몸체 방향, 속도, 위치, 관절 상태, 접촉 상태 및 불확실성을 추정한다.

접촉 추정(Contact Estimation)은 많은 제어 알고리즘이 어떤 발이 로봇을 지지하고 있는지를 알아야 하기 때문에 특히 중요하다. 명령된 스탠스 상태(Stance State)가 실제 접촉을 보장하는 것은 아니며 불규칙한 지형에서는 이러한 차이가 더욱 커질 수 있다. 접촉 추정기는 발 힘, 모터 토크, 관절 운동, 관성 측정값 및 계획된 보행 위상(Gait Phase)을 사용할 수 있다. 신뢰성 높은 접촉 정보는 상태 추정, 미끄러짐 감지, 보행 전환 및 지면 반력 제어를 지원한다.

로봇 모델 계층(Robot Model Layer)은 운동학, 동역학, 관절 제한, 관성 특성, 충돌 형상 및 액추에이터 성능에 대한 공통 표현을 제공한다. 순기구학(Forward Kinematics), 역기구학(Inverse Kinematics), 자코비안(Jacobian), 강체 동역학(Rigid-Body Dynamics) 및 좌표 변환은 일관된 모델 파라미터를 사용해야 한다. 공통 모델을 유지하면 상태 추정, 계획, 시뮬레이션 및 제어 모듈 사이에서 서로 다른 가정이 사용되어 발생할 수 있는 미세한 불일치를 방지할 수 있다.

보행 제어 계층(Locomotion Control Layer)은 원하는 몸체 및 발의 동작을 동역학적으로 실행 가능한 액추에이터 명령으로 변환한다. 아키텍처에 따라 이 계층에는 모델 예측 제어(Model Predictive Control), 전신 제어(Whole-Body Control), 역동역학(Inverse Dynamics), 임피던스 제어(Impedance Control) 또는 학습된 정책(Learned Policy)이 포함될 수 있다. 이 계층은 로봇과 환경의 물리적 제약을 만족하면서 몸체 방향, 무게중심 거동, 발 궤적, 접촉력 및 관절 운동을 제어한다.

보행 관리 계층(Gait-Management Layer)은 네 개 다리의 스탠스 단계(Stance Phase)와 스윙 단계(Swing Phase)의 시간적 패턴을 결정한다. 걷기, 트로팅(Trotting), 페이싱(Pacing), 바운딩(Bounding) 및 기타 보행은 접촉 스케줄(Contact Schedule), 위상 변수(Phase Variable), 듀티 팩터(Duty Factor) 및 전환 규칙을 통해 표현할 수 있다. 보행 관리자는 궤적 생성기와 예측 제어기에 미래 접촉 정보를 제공하면서 보행 모드 사이의 부드러운 전환을 조정한다.

발 궤적 생성(Foot Trajectory Generation)은 보행 타이밍과 목표 발 디딤 위치(Foothold Target)를 연속적인 스윙 다리 운동으로 변환한다. 궤적은 지형과의 충돌을 피할 수 있도록 발을 충분히 들어 올리고 원하는 접촉 위치로 이동시킨 후 적절한 속도로 지면에 접근시켜야 한다. 또한 관절 작업공간 및 속도 제한을 만족해야 한다. 피드백 보정(Feedback Correction)을 통해 몸체 속도 오차나 예상하지 못한 지형 상호작용에 대응하여 기준 궤적을 수정할 수 있다.

발 디딤 계획(Foothold Planning)은 기본적인 궤적 생성보다 상위에서 동작하며 적절한 미래 접촉 위치를 선택한다. 평탄한 지형에서는 주로 원하는 속도와 보행 기하학을 이용하여 발 디딤 위치를 생성할 수 있다. 험지에서는 플래너가 고도, 경사, 장애물, 표면 품질, 도달 가능성 및 안정성 정보를 함께 고려해야 한다. 선택된 발 디딤 위치는 지형 인식(Terrain Perception)과 동적 보행 제어기 사이의 핵심 인터페이스가 된다.

인식 계층(Perception Layer)은 카메라, 깊이 카메라(Depth Camera), 라이다, 레이더 또는 특수 거리 측정 장치와 같은 외수용성 센서(Exteroceptive Sensor)를 처리한다. 이 계층은 환경의 기하학적 구조를 추정하고 보행에 필요한 지형 특성을 식별한다. 응용 분야에 따라 인식 시스템은 포인트 클라우드(Point Cloud), 고도 지도(Elevation Map), 주행 가능성 지도(Traversability Map), 의미론적 레이블(Semantic Label), 장애물, 계단, 경계 또는 이후 계획 모듈에서 사용할 후보 지지 표면을 생성할 수 있다.

지형 표현(Terrain Representation)은 인식과 보행 계획을 연결한다. 원시 센서 측정값은 일반적으로 고주파 제어기에서 직접 사용하기에는 데이터 크기가 크고 잡음이 많으므로 지역 고도 지도(Local Elevation Map) 또는 주행 가능성 격자(Traversability Grid)와 같은 압축된 표현으로 변환한다. 이러한 표현은 로봇이 이동함에 따라 일관된 좌표와 불확실성 추정치를 유지하면서 갱신되어야 한다. 이후 지형 정보는 발 디딤 위치 선택과 몸체 궤적 계획을 안내할 수 있다.

지역 운동 계획 계층(Local Motion-Planning Layer)은 로봇이 주변 환경에서 어떻게 움직여야 하는지를 결정한다. 이 계층은 장애물과 지형을 고려하면서 내비게이션 목표를 원하는 몸체 속도, 진행 방향, 자세 또는 단기 궤적으로 변환한다. 다리형 로봇에서는 플랫폼을 단순한 평면 이동 베이스로 취급하기보다 몸체 여유 공간(Body Clearance), 경사 한계, 스텝 능력 및 실행 가능한 접촉 영역까지 지역 계획에 포함할 수 있다.

전역 내비게이션(Global Navigation)은 더 긴 공간적 및 시간적 범위에서 동작한다. 지도, 위치 추정(Localization), 임무 목표 및 환경 제약을 사용하여 환경을 통과하는 경로를 결정한다. 생성된 경로는 지역 계획으로 전달되고 지역 계획은 현재 지형과 로봇 상태에 맞게 이를 조정한다. 이러한 분리를 통해 전역 수준의 추론은 상대적으로 느리게 수행하면서 지역 계획과 보행은 즉각적인 외란과 새롭게 관측된 장애물에 빠르게 대응할 수 있다.

행동 및 임무 계층(Behavior and Mission Layer)은 검사 지점으로 이동, 작업자 추종, 지정된 영역 진입, 센싱 작업 수행 또는 충전 스테이션 복귀와 같은 상위 수준의 작업을 조정한다. 상태 머신(State Machine), 행동 트리(Behavior Tree), 작업 플래너(Task Planner) 또는 정책 기반 시스템을 사용할 수 있다. 이러한 계층은 개별 관절을 직접 명령하는 대신 목표와 제약조건을 전달함으로써 임무 논리와 물리적 제어 사이의 분리를 유지해야 한다.

계층 사이의 통신에는 지연시간 요구조건에 따라 공유 메모리(Shared Memory), 메시지 전달(Message Passing), 발행-구독 미들웨어(Publish-Subscribe Middleware) 또는 직접 실시간 인터페이스를 사용할 수 있다. 고주파 토크와 상태 데이터는 낮은 지연시간을 갖는 결정론적 경로를 사용해야 하지만 지도, 임무 명령 및 진단 정보는 상대적으로 느린 비동기 통신을 사용할 수 있다. 시간 중요도에 따라 통신 메커니즘을 선택하면 상위 소프트웨어 활동이 보행 제어를 방해하는 것을 방지할 수 있다.

사족보행 로봇 제어는 여러 센서와 프로세서에서 생성된 측정값을 결합하므로 시간 동기화(Time Synchronization)가 필수적이다. 인코더 상태, 관성 측정값, 힘 데이터, 카메라 프레임 및 라이다 스캔은 정확한 획득 시각과 연결되어야 한다. 타임스탬프(Timestamp) 오차는 실제로 존재하지 않는 움직임처럼 나타나 센서 융합 성능을 저하시킬 수 있다. 따라서 하드웨어 클록, 동기화된 타임스탬프, 버퍼링 및 보간(Interpolation)은 단순한 로깅 편의 기능이 아니라 중요한 아키텍처 구성요소이다.

안전 계층(Safety Layer)은 하나의 상위 모듈로만 존재하는 것이 아니라 전체 아키텍처에 걸쳐 적용되어야 한다. 저수준 보호 기능은 관절 제한, 전류, 전압, 온도, 통신 손실 및 액추에이터 고장을 감시한다. 상위 수준 감독 기능은 몸체 방향, 전도 상태(Fall Condition), 위치 추정 품질, 지형 위험 및 플래너 고장을 감시한다. 안전 대응에는 토크 제한, 제어된 정지, 자세 복구, 모터 차단 또는 사전에 정의된 안전 상태로의 전환이 포함될 수 있다.

고장 관리(Fault Management)는 복구 가능한 외란과 시스템 정지가 필요한 고장을 구분할 수 있어야 한다. 일시적인 발 미끄러짐, 지연된 인식 또는 잘못된 한 번의 스텝은 피드백과 재계획을 통해 처리할 수 있지만 액추에이터 과열이나 통신 손실은 성능 제한 운용(Degraded Operation) 또는 비상 정지가 필요할 수 있다. 진단 정보는 상위 계층으로 전달되어 행동 논리가 시스템의 실제 능력을 이해하고 실행 불가능한 동작을 계속 요구하지 않도록 해야 한다.

시뮬레이션(Simulation)은 가능한 경우 실제 로봇과 동일한 인터페이스를 재현해야 한다. 공통 하드웨어 추상화 계층을 기반으로 개발된 제어기는 구조적인 변경을 최소화하면서 물리 시뮬레이션과 실제 하드웨어에서 모두 동작할 수 있다. 시뮬레이션은 실제 시스템에서 재현하기에 비용이 높거나 위험할 수 있는 보행, 외란, 지형, 액추에이터 제한 및 고장 조건을 반복적으로 시험할 수 있도록 한다.

로깅(Logging)과 관측 가능성(Observability)은 복잡한 다리형 로봇 시스템을 개발하는 데 필수적이다. 주요 상태, 명령, 센서 측정값, 접촉 추정, 플래너 출력, 타이밍 정보 및 고장 이벤트를 동기화된 타임스탬프와 함께 기록해야 한다. 시각화 및 재생 도구(Replay Tool)를 이용하면 엔지니어가 고장 상황을 재구성하고 예상된 거동과 실제 거동을 비교할 수 있다. 체계적인 관측 가능성이 없으면 간헐적으로 발생하는 동적 불안정성을 디버깅하기가 매우 어렵다.

구성 관리(Configuration Management)는 소프트웨어 모듈이 일관된 파라미터를 사용하도록 보장한다. 로봇 치수, 질량, 관절 제한, 제어기 게인(Controller Gain), 센서 보정값, 보행 파라미터 및 안전 임계값은 버전 관리되어야 하며 특정 하드웨어 구성과 연결되어야 한다. 여러 모듈에 파라미터가 통제되지 않은 상태로 중복되면 미세한 오류가 발생할 수 있다. 따라서 중앙집중식 또는 명확하게 관리되는 구성 시스템은 소프트웨어 아키텍처의 중요한 부분을 형성한다.

기계학습(Machine Learning) 구성요소는 전체 아키텍처를 대체하지 않으면서 여러 계층에 통합될 수 있다. 학습 기반 추정기(Learned Estimator)는 접촉 또는 지형 특성을 추론할 수 있고, 학습 기반 보행 정책(Learned Locomotion Policy)은 관절 또는 발 명령을 생성할 수 있으며, 의미론적 모델(Semantic Model)은 내비게이션을 지원할 수 있다. 그러나 결정론적 상태 추정, 제어 및 안전 기능과 함께 동작할 수 있도록 입력, 출력, 실행 주기, 고장 처리 및 물리적 제약조건을 명확하게 정의해야 한다.

컴퓨팅 배치(Computational Deployment)는 여러 프로세서에 걸쳐 구성되는 경우가 많다. 모터 제어기 또는 마이크로컨트롤러(Microcontroller)는 하드 실시간 액추에이터 루프(Hard Real-Time Actuator Loop)를 처리하고, 온보드 중앙처리장치(CPU)는 상태 추정, 계획 및 시스템 관리를 실행한다. 그래픽처리장치(GPU) 또는 가속기(Accelerator)는 인식과 학습된 정책을 처리할 수 있다. 따라서 소프트웨어 아키텍처는 프로세서 경계, 통신 지연, 데이터 소유권, 동기화, 자원 경합(Resource Contention) 및 개별 컴퓨팅 구성요소가 사용할 수 없게 되었을 때의 안전한 동작을 고려해야 한다.

성공적인 사족보행 로봇 소프트웨어 아키텍처는 궁극적으로 모듈의 개수가 아니라 각 모듈의 책임과 인터페이스가 얼마나 명확하게 정의되어 있는지에 의해 결정된다. 하드웨어 추상화, 상태 추정, 모델링, 보행 생성, 보행 제어, 인식, 계획, 내비게이션, 임무 논리, 안전, 시뮬레이션 및 진단 기능은 적절한 시간 척도(Time Scale)에서 동작하면서 일관된 로봇 및 환경 상태 정보를 공유해야 한다.

계층형 접근법(Layered Approach)은 실시간 성능과 시스템 확장성을 유지하면서 이러한 복잡성을 관리하기 위한 실용적인 프레임워크를 제공한다. 빠른 내부 루프(Inner Loop)는 물리적 안정성을 유지하고, 중간 계층은 접촉과 보행을 조정하며, 상대적으로 느린 상위 계층은 지형과 임무 목표를 해석한다. 이러한 계층을 명확한 인터페이스와 동기화된 상태 정보로 연결함으로써 사족보행 로봇은 상위 수준의 의도(High-Level Intent)를 안전하고 동역학적으로 실행 가능한 물리적 행동으로 변환할 수 있다.

##  

## 01.06. Contact Mechanics Friction Cone Slip Model [w/Code]

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

Contact mechanics describes how forces are transmitted between a quadruped foot and the terrain during stance, touchdown, and slip. Because legged locomotion depends on intermittent environmental contacts, the quality of these interactions directly determines balance, acceleration, turning, and disturbance rejection. A useful contact model must represent normal support, tangential friction, impact, compliance, and possible loss of contact.

The simplest rigid contact model assumes that the foot and terrain do not penetrate each other. Let the normal gap between the foot and surface be represented by g. Valid contact requires g ≥ 0, while the normal contact force fn must satisfy fn ≥ 0 because an ordinary ground surface can push the foot but cannot pull it. These unilateral conditions distinguish contact mechanics from conventional bilateral mechanical constraints.

Contact complementarity expresses the relationship between separation and normal force. Conceptually, gfn = 0 means that either the foot is separated from the terrain and the normal force is zero, or the foot is touching the terrain and a compressive force may exist. Such complementarity conditions are useful in contact-implicit trajectory optimization and physics simulation because the contact sequence does not always need to be prescribed in advance.

When a stance foot remains stationary relative to rigid terrain, its contact velocity is approximately zero. Using the contact Jacobian Jc, this condition can be expressed as Jc(q)q̇ = 0. An acceleration-level constraint can be obtained by differentiation. These equations connect foot-ground constraints to full-body dynamics and allow inverse dynamics or whole-body controllers to compute motions and forces consistent with active contacts.

The total ground reaction force can be decomposed into a normal component and tangential components. The normal force supports body weight and contributes to vertical acceleration, while tangential forces generate propulsion, braking, and turning. The maximum sustainable tangential force depends strongly on the available normal force and the friction properties of the foot-terrain interface.

Coulomb friction provides a widely used approximation for dry contact. In its simplest form, the tangential force magnitude must satisfy \|\|ft\|\| ≤ μfn, where μ is the coefficient of friction, ft is the tangential force, and fn is the normal force. This inequality defines the range of contact forces that can be generated without gross sliding and forms a central physical constraint in quadruped locomotion control.

In three-dimensional contact, the Coulomb inequality defines a friction cone whose axis is aligned with the terrain normal. Contact forces inside the cone are compatible with sticking contact, while forces attempting to move outside the cone cannot generally be maintained without slip. Increasing normal force expands the allowable tangential force region, whereas a low-friction surface produces a narrow cone and severely limits horizontal force generation.

Optimization-based controllers often approximate the nonlinear friction cone with a friction pyramid. Linear inequalities bound the tangential force components relative to the normal force, producing a polyhedral approximation that is computationally convenient for quadratic programming and model predictive control. More pyramid faces improve approximation accuracy but increase the number of constraints that must be evaluated during optimization.

The coefficient of friction is not a universal constant for a robot foot. It depends on foot material, terrain material, surface roughness, contamination, moisture, temperature, normal loading, and sliding conditions. Rubber on dry concrete may provide strong traction, while the same foot on wet metal, dust, ice, loose gravel, or mud can behave very differently. Robust locomotion should therefore avoid assuming an unrealistically precise friction value.

Static and kinetic friction describe different contact regimes. Static friction resists relative motion while the foot remains stuck to the surface, up to a limiting value. Once sliding begins, kinetic friction governs the resisting force and may have a different magnitude. The transition between these regimes can be abrupt in an ideal Coulomb model, although real materials usually exhibit more complicated velocity-dependent behavior.

Slip occurs when the contact can no longer maintain the assumed no-motion condition. This may happen because commanded tangential force exceeds available friction, normal force becomes too small, terrain deforms, or an unexpected disturbance changes loading. Slip invalidates many stance assumptions used by state estimators and controllers, making rapid detection and adaptation important for preventing a local contact failure from becoming a full-body fall.

Slip velocity is the relative tangential velocity between the foot and terrain at the contact point. Under ideal sticking conditions it is approximately zero. Persistent nonzero tangential velocity while normal contact remains active indicates sliding. In practice, slip can be estimated by combining leg kinematics, body-state estimates, inertial sensing, force measurements, motor torque information, and exteroceptive observations of terrain-relative motion.

Incipient slip is especially important because corrective action is most effective before large sliding develops. A controller can monitor the ratio between tangential force and available friction capacity. As the commanded force approaches the friction boundary, the contact margin decreases. Force redistribution among other stance feet, body acceleration reduction, gait modification, or posture adjustment can restore margin before the foot begins substantial sliding.

A friction margin provides a useful robustness measure. Rather than operating directly on the theoretical friction-cone boundary, controllers maintain contact forces safely inside it. This accounts for uncertainty in friction coefficient, force estimation, terrain orientation, and dynamic modeling. Larger margins improve robustness but reduce the acceleration and maneuvering performance that can be extracted from the available contacts.

Terrain orientation changes the interpretation of contact forces. On a slope, the contact normal is not aligned with the gravity direction, so part of the gravitational load acts tangentially to the surface. The robot must generate sufficient friction merely to remain stationary. As slope angle increases, the required tangential-to-normal force ratio grows, eventually approaching the available friction limit even without commanded locomotion.

Foot geometry influences the contact model. A small rounded foot can often be approximated as a point contact capable of transmitting force but limited moment. A larger flat foot produces a finite contact patch and may support moments depending on pressure distribution and rotational friction. Quadruped models frequently use point contacts for computational simplicity, but this assumption should reflect the actual mechanical design and terrain interaction.

Soft feet and deformable terrain violate the ideal rigid-contact assumption. Rubber pads, soil, sand, mud, vegetation, or snow can deform significantly under load. Contact force then depends on penetration, deformation rate, contact area, and material properties. Compliance can reduce impact forces and improve adaptation to irregular surfaces, but it introduces additional states and uncertainty into estimation and control.

A compliant normal-contact model may represent force as a function of penetration depth and penetration velocity. Spring-damper formulations are commonly used in simulation, where stiffness represents resistance to deformation and damping dissipates impact energy. These models avoid instantaneous rigid impacts but require careful parameter selection because excessive stiffness creates numerical difficulty while insufficient stiffness allows unrealistic penetration.

Tangential compliance can also occur before macroscopic slip. Rubber feet may deform elastically under shear loading while remaining attached to the terrain. This produces small relative displacements that are not equivalent to full sliding. More advanced contact models can represent this presliding behavior, hysteresis, and velocity-dependent friction, although simpler Coulomb models are often preferred for real-time optimization because of their computational efficiency.

Touchdown introduces impact dynamics because the foot velocity may change rapidly when contact is established. An ideal rigid impact can be represented using impulses that instantaneously modify generalized velocity while satisfying contact constraints. Real quadrupeds reduce impact severity through foot compliance, structural flexibility, actuator backdrivability, controlled touchdown velocity, and active impedance control rather than relying on perfectly rigid collision behavior.

Liftoff occurs when the normal contact force decreases toward zero and the foot transitions from stance to swing. Maintaining an artificial contact constraint after normal force vanishes would produce physically invalid pulling forces. Contact-aware controllers therefore coordinate force unloading with gait timing so that a leg gradually reduces its support contribution before entering swing, particularly during smooth gait transitions.

Multiple simultaneous contacts create a force-distribution problem. During a four-foot or three-foot stance, many combinations of individual contact forces can produce the same net body wrench. Optimization can distribute forces while keeping every foot inside its friction limits, respecting unilateral normal forces, minimizing actuator effort, and maintaining adequate contact margins. This redundancy is a major advantage of multi-legged locomotion.

Contact uncertainty should be explicitly considered in rough-terrain operation. Surface normal estimates may be inaccurate, friction may vary between neighboring footholds, and loose terrain may move after loading. A foothold that appears geometrically safe may therefore have poor mechanical support. Combining terrain perception with online contact observations allows the robot to update its assumptions after each touchdown and adapt subsequent steps.

Friction estimation can be performed indirectly from observed contact behavior. If measured tangential and normal forces are available, the robot can infer lower bounds on usable friction while contacts remain stable and update estimates when slip occurs. However, aggressive probing can itself destabilize the robot. Practical systems therefore combine conservative prior assumptions, terrain classification, measured forces, and gradual online adaptation.

Contact models used for planning and control need not have identical complexity. A planner may use simplified friction cones and rigid point contacts to achieve fast prediction, while a simulator may include compliant contact and detailed collision geometry. Low-level controllers can compensate for remaining modeling errors through feedback. Selecting model complexity according to the computational layer provides a useful balance between physical fidelity and real-time performance.

Reliable quadruped locomotion ultimately depends on maintaining physically valid contact rather than merely generating desired joint trajectories. Normal-force constraints, friction cones, slip behavior, terrain orientation, compliance, impact, and uncertainty determine which body motions can actually be supported by the environment. Contact-aware planning and control transform these mechanical limits into explicit constraints for safe and dynamically feasible locomotion.

접촉 역학(Contact Mechanics)은 스탠스(Stance), 착지(Touchdown), 미끄러짐(Slip) 과정에서 사족보행 로봇의 발과 지형 사이에 힘이 어떻게 전달되는지를 설명한다. 다리형 보행은 환경과의 간헐적인 접촉(Intermittent Contact)에 의존하므로 이러한 상호작용의 품질은 균형, 가속, 회전 및 외란 억제(Disturbance Rejection)를 직접적으로 결정한다. 유용한 접촉 모델(Contact Model)은 수직 지지력, 접선 마찰, 충격, 컴플라이언스(Compliance), 접촉 상실 가능성을 표현할 수 있어야 한다.

가장 단순한 강체 접촉 모델(Rigid Contact Model)은 발과 지형이 서로 관통하지 않는다고 가정한다. 발과 표면 사이의 수직 간격(Normal Gap)을 g로 나타내면 유효한 접촉은 g ≥ 0을 만족해야 하며, 수직 접촉력(Normal Contact Force) fn은 fn ≥ 0을 만족해야 한다. 일반적인 지면은 발을 밀어낼 수 있지만 끌어당길 수 없기 때문이다. 이러한 단방향 조건(Unilateral Condition)은 접촉 역학을 일반적인 양방향 기계적 구속조건(Bilateral Mechanical Constraint)과 구별한다.

접촉 상보성(Contact Complementarity)은 분리 상태와 수직력 사이의 관계를 표현한다. 개념적으로 gfn = 0은 발이 지형에서 떨어져 있을 때 수직력이 0이거나, 발이 지형에 접촉해 있을 때 압축력이 존재할 수 있음을 의미한다. 이러한 상보성 조건(Complementarity Condition)은 접촉 순서를 항상 사전에 지정할 필요가 없기 때문에 접촉 내재형 궤적 최적화(Contact-Implicit Trajectory Optimization)와 물리 시뮬레이션(Physics Simulation)에서 유용하다.

스탠스 발(Stance Foot)이 강체 지형에 대해 정지된 상태를 유지하면 접촉점의 속도는 대략 0이다. 접촉 자코비안(Contact Jacobian) Jc를 사용하면 이러한 조건을 Jc(q)q̇ = 0으로 표현할 수 있다. 이를 미분하면 가속도 수준의 구속조건(Acceleration-Level Constraint)을 얻을 수 있다. 이러한 방정식은 발-지면 구속조건을 전신 동역학(Full-Body Dynamics)과 연결하며 역동역학(Inverse Dynamics)이나 전신 제어기(Whole-Body Controller)가 활성 접촉과 일관된 움직임 및 힘을 계산하도록 한다.

전체 지면 반력(Ground Reaction Force)은 수직 성분과 접선 성분으로 분해할 수 있다. 수직력은 몸체의 무게를 지지하고 수직 가속도에 기여하며, 접선력(Tangential Force)은 추진, 제동 및 회전을 발생시킨다. 유지할 수 있는 최대 접선력은 사용 가능한 수직력과 발-지형 인터페이스(Foot-Terrain Interface)의 마찰 특성에 크게 의존한다.

쿨롱 마찰(Coulomb Friction)은 건식 접촉(Dry Contact)을 표현하기 위해 널리 사용되는 근사 모델이다. 가장 단순한 형태에서 접선력의 크기는 \|\|ft\|\| ≤ μfn을 만족해야 하며, 여기에서 μ는 마찰계수(Coefficient of Friction), ft는 접선력, fn은 수직력을 나타낸다. 이 부등식은 큰 미끄러짐 없이 생성할 수 있는 접촉력의 범위를 정의하며 사족보행 로봇의 보행 제어에서 핵심적인 물리적 제약조건을 형성한다.

3차원 접촉에서 쿨롱 마찰 부등식은 지형 법선(Terrain Normal)을 축으로 하는 마찰 원뿔(Friction Cone)을 정의한다. 원뿔 내부의 접촉력은 고착 접촉(Sticking Contact)과 양립할 수 있지만 원뿔 외부로 벗어나려는 힘은 일반적으로 미끄러짐 없이 유지할 수 없다. 수직력이 증가하면 허용 가능한 접선력 영역이 확대되는 반면, 저마찰 표면에서는 원뿔이 좁아져 수평 방향 힘 생성 능력이 크게 제한된다.

최적화 기반 제어기(Optimization-Based Controller)는 비선형 마찰 원뿔을 마찰 피라미드(Friction Pyramid)로 근사하는 경우가 많다. 선형 부등식을 이용하여 수직력에 대한 접선력 성분을 제한함으로써 이차 계획법(Quadratic Programming)과 모델 예측 제어(Model Predictive Control)에서 계산하기 편리한 다면체 근사(Polyhedral Approximation)를 생성한다. 피라미드 면의 수를 늘리면 근사 정확도는 향상되지만 최적화 과정에서 평가해야 하는 제약조건의 수도 증가한다.

마찰계수는 로봇 발에 대해 항상 일정한 보편적 상수가 아니다. 발 재질, 지형 재질, 표면 거칠기, 오염, 습기, 온도, 수직 하중 및 미끄러짐 조건에 따라 달라진다. 건조한 콘크리트 위의 고무는 높은 접지력(Traction)을 제공할 수 있지만 동일한 발이라도 젖은 금속, 먼지, 얼음, 느슨한 자갈 또는 진흙 위에서는 매우 다르게 동작할 수 있다. 따라서 강건한 보행에서는 비현실적으로 정확한 하나의 마찰계수를 가정해서는 안 된다.

정지 마찰(Static Friction)과 운동 마찰(Kinetic Friction)은 서로 다른 접촉 상태를 설명한다. 정지 마찰은 발이 표면에 고정된 상태에서 상대 운동에 저항하며 특정 한계값까지 증가할 수 있다. 미끄러짐이 시작되면 운동 마찰이 저항력을 결정하며 그 크기는 정지 마찰과 다를 수 있다. 이상적인 쿨롱 모델에서는 두 상태 사이의 전환이 급격할 수 있지만 실제 재료에서는 일반적으로 더욱 복잡한 속도 의존적 거동이 나타난다.

미끄러짐(Slip)은 접촉이 더 이상 가정된 무운동 조건(No-Motion Condition)을 유지할 수 없을 때 발생한다. 명령된 접선력이 사용 가능한 마찰력을 초과하거나, 수직력이 지나치게 작아지거나, 지형이 변형되거나, 예상하지 못한 외란이 하중 상태를 변화시키는 경우에 발생할 수 있다. 미끄러짐은 상태 추정기(State Estimator)와 제어기가 사용하는 여러 스탠스 가정을 무효화하므로 국부적인 접촉 실패가 전신 전도(Fall)로 이어지는 것을 방지하기 위해 신속한 감지와 적응이 중요하다.

미끄러짐 속도(Slip Velocity)는 접촉점에서 발과 지형 사이의 상대적인 접선 속도를 의미한다. 이상적인 고착 조건에서는 이 값이 거의 0이다. 수직 접촉이 유지되는 동안 지속적으로 0이 아닌 접선 속도가 나타난다면 미끄러짐을 의미한다. 실제 시스템에서는 다리 운동학, 몸체 상태 추정, 관성 센싱, 힘 측정, 모터 토크 정보 및 지형에 대한 상대 운동의 외수용성 관측(Exteroceptive Observation)을 결합하여 미끄러짐을 추정할 수 있다.

초기 미끄러짐(Incipient Slip)은 큰 미끄러짐이 발생하기 전에 보정 동작을 수행하는 것이 가장 효과적이라는 점에서 특히 중요하다. 제어기는 접선력과 사용 가능한 마찰력 사이의 비율을 감시할 수 있다. 명령된 힘이 마찰 경계에 가까워질수록 접촉 여유(Contact Margin)는 감소한다. 다른 스탠스 발로의 힘 재분배, 몸체 가속도 감소, 보행 패턴 수정 또는 자세 조정을 통해 발이 크게 미끄러지기 전에 접촉 여유를 회복할 수 있다.

마찰 여유(Friction Margin)는 강건성을 평가하기 위한 유용한 척도를 제공한다. 제어기는 이론적인 마찰 원뿔의 경계에서 직접 동작하는 대신 접촉력을 원뿔 내부에 안전하게 유지한다. 이를 통해 마찰계수, 힘 추정, 지형 방향 및 동역학 모델링의 불확실성을 고려할 수 있다. 더 큰 여유는 강건성을 향상시키지만 사용 가능한 접촉으로부터 얻을 수 있는 가속 및 기동 성능은 감소시킨다.

지형 방향(Terrain Orientation)은 접촉력의 해석을 변화시킨다. 경사면에서는 접촉 법선이 중력 방향과 일치하지 않으므로 중력 하중의 일부가 표면의 접선 방향으로 작용한다. 따라서 로봇이 정지 상태를 유지하기 위해서도 충분한 마찰력을 생성해야 한다. 경사각이 증가할수록 필요한 접선력과 수직력의 비율이 증가하며, 명령된 보행이 없더라도 결국 사용 가능한 마찰 한계에 가까워질 수 있다.

발 형상(Foot Geometry)은 접촉 모델에 영향을 미친다. 작고 둥근 발은 힘을 전달할 수 있지만 모멘트 전달은 제한되는 점 접촉(Point Contact)으로 근사할 수 있다. 더 크고 평평한 발은 유한한 접촉 면적(Contact Patch)을 형성하며 압력 분포와 회전 마찰에 따라 모멘트를 지지할 수도 있다. 사족보행 로봇 모델에서는 계산 단순화를 위해 점 접촉을 자주 사용하지만 이러한 가정은 실제 기계적 설계와 지형 상호작용을 적절하게 반영해야 한다.

부드러운 발과 변형 가능한 지형(Deformable Terrain)은 이상적인 강체 접촉 가정을 만족하지 않는다. 고무 패드, 토양, 모래, 진흙, 식생 또는 눈은 하중을 받으면 상당히 변형될 수 있다. 이 경우 접촉력은 침투 깊이(Penetration Depth), 변형 속도, 접촉 면적 및 재료 특성에 따라 달라진다. 컴플라이언스는 충격력을 감소시키고 불규칙한 표면에 대한 적응성을 향상시킬 수 있지만 상태 추정과 제어에 추가적인 상태 변수와 불확실성을 도입한다.

유연한 수직 접촉 모델(Compliant Normal-Contact Model)은 접촉력을 침투 깊이와 침투 속도의 함수로 표현할 수 있다. 스프링-댐퍼 모델(Spring-Damper Model)은 시뮬레이션에서 일반적으로 사용되며 강성은 변형에 대한 저항을, 감쇠(Damping)는 충격 에너지의 소산을 나타낸다. 이러한 모델은 순간적인 강체 충격을 피할 수 있지만 지나치게 높은 강성은 수치 계산을 어렵게 하고 너무 낮은 강성은 비현실적인 침투를 허용하므로 신중한 파라미터 선정이 필요하다.

거시적인 미끄러짐이 발생하기 전에도 접선 컴플라이언스(Tangential Compliance)가 나타날 수 있다. 고무 발은 지형에 부착된 상태를 유지하면서 전단 하중(Shear Loading)에 의해 탄성적으로 변형될 수 있다. 이는 완전한 미끄러짐과는 다른 작은 상대 변위를 발생시킨다. 보다 발전된 접촉 모델은 이러한 미끄러짐 이전 거동(Presliding Behavior), 히스테리시스(Hysteresis) 및 속도 의존 마찰을 표현할 수 있지만 실시간 최적화에서는 계산 효율성 때문에 단순한 쿨롱 모델을 사용하는 경우가 많다.

착지(Touchdown) 시에는 접촉이 형성되면서 발 속도가 급격하게 변화할 수 있기 때문에 충격 동역학(Impact Dynamics)이 발생한다. 이상적인 강체 충격은 접촉 제약을 만족하면서 일반화 속도를 순간적으로 변화시키는 충격량(Impulse)을 이용하여 표현할 수 있다. 실제 사족보행 로봇은 완전한 강체 충돌에 의존하기보다 발의 컴플라이언스, 구조적 유연성, 액추에이터 역구동성, 제어된 착지 속도 및 능동 임피던스 제어(Active Impedance Control)를 통해 충격을 감소시킨다.

이륙(Liftoff)은 수직 접촉력이 0에 가까워지고 발이 스탠스 상태에서 스윙 상태로 전환될 때 발생한다. 수직력이 사라진 이후에도 인위적인 접촉 제약을 유지하면 물리적으로 불가능한 당기는 힘이 생성될 수 있다. 따라서 접촉 인식 제어기(Contact-Aware Controller)는 보행 타이밍과 힘 제거를 조정하여 다리가 스윙 상태로 진입하기 전에 지지 기여도를 점진적으로 감소시킨다. 이는 특히 부드러운 보행 전환에서 중요하다.

여러 개의 동시 접촉(Multiple Simultaneous Contacts)은 힘 분배 문제(Force-Distribution Problem)를 발생시킨다. 네 발 또는 세 발이 동시에 지면을 지지하는 경우 각각의 접촉력에 대한 여러 조합이 동일한 몸체의 합력 및 합모멘트(Net Body Wrench)를 생성할 수 있다. 최적화를 이용하면 각 발의 힘을 마찰 한계 내부에 유지하고, 단방향 수직력 조건을 만족하며, 액추에이터 노력을 최소화하고, 충분한 접촉 여유를 유지하도록 힘을 분배할 수 있다. 이러한 중복성은 다족 보행(Multi-Legged Locomotion)의 중요한 장점이다.

험지 운용에서는 접촉 불확실성(Contact Uncertainty)을 명시적으로 고려해야 한다. 표면 법선 추정값이 부정확할 수 있고, 인접한 발 디딤 위치 사이에서도 마찰이 달라질 수 있으며, 느슨한 지형은 하중을 받은 후 움직일 수 있다. 따라서 기하학적으로 안전해 보이는 발 디딤 위치라도 기계적으로 불충분한 지지력을 가질 수 있다. 지형 인식과 온라인 접촉 관측을 결합하면 로봇은 각 착지 이후 자신의 가정을 갱신하고 이후 스텝을 적응적으로 수정할 수 있다.

마찰 추정(Friction Estimation)은 관측된 접촉 거동으로부터 간접적으로 수행할 수 있다. 접선력과 수직력의 측정값을 사용할 수 있다면 로봇은 접촉이 안정적으로 유지되는 동안 사용 가능한 마찰의 하한을 추론하고 미끄러짐이 발생했을 때 추정값을 갱신할 수 있다. 그러나 공격적인 마찰 탐색 자체가 로봇을 불안정하게 만들 수 있다. 따라서 실제 시스템에서는 보수적인 사전 가정, 지형 분류, 측정된 힘 및 점진적인 온라인 적응(Online Adaptation)을 결합한다.

계획과 제어에서 사용하는 접촉 모델이 반드시 동일한 복잡도를 가질 필요는 없다. 플래너(Planner)는 빠른 예측을 위해 단순화된 마찰 원뿔과 강체 점 접촉을 사용할 수 있는 반면, 시뮬레이터는 유연한 접촉과 상세한 충돌 형상을 포함할 수 있다. 저수준 제어기(Low-Level Controller)는 피드백을 통해 남아 있는 모델링 오차를 보상할 수 있다. 계산 계층에 따라 모델의 복잡도를 선택하면 물리적 충실도(Physical Fidelity)와 실시간 성능 사이에서 효과적인 균형을 얻을 수 있다.

신뢰성 높은 사족보행 로봇의 보행은 궁극적으로 원하는 관절 궤적을 생성하는 것만이 아니라 물리적으로 유효한 접촉(Physically Valid Contact)을 유지하는 것에 달려 있다. 수직력 제약, 마찰 원뿔, 미끄러짐 거동, 지형 방향, 컴플라이언스, 충격 및 불확실성은 환경이 실제로 어떤 몸체 움직임을 지지할 수 있는지를 결정한다. 접촉 인식 계획 및 제어(Contact-Aware Planning and Control)는 이러한 기계적 한계를 명시적인 제약조건으로 변환하여 안전하고 동역학적으로 실행 가능한 보행을 구현한다.

##  

## 01.07. State Estimation for Quadruped IMU Kinematics [w/Code]

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

State estimation for a quadruped reconstructs the robot's body orientation, position, velocity, joint configuration, and contact condition from imperfect sensor measurements. Reliable estimates are essential because locomotion controllers cannot directly observe the complete physical state. Unlike wheeled robots, quadrupeds repeatedly change supporting contacts, making estimation strongly coupled with leg kinematics and contact reasoning.

The inertial measurement unit, or IMU, is a primary sensor for estimating body motion. A typical IMU contains three-axis gyroscopes and accelerometers, and some systems additionally use magnetometers. Gyroscopes measure angular velocity, while accelerometers measure specific force rather than pure translational acceleration. These measurements provide high-rate motion information but contain bias, noise, scale errors, and temperature-dependent effects.

Body orientation can be propagated by integrating measured angular velocity. Rotation matrices or unit quaternions are commonly used because quadrupeds may experience large roll, pitch, and yaw motions during locomotion or recovery. Gyroscope integration provides excellent short-term orientation tracking, but even a small angular-rate bias accumulates over time and produces orientation drift if no additional observations are introduced.

Accelerometers provide information that can help constrain orientation relative to gravity. During static or slowly accelerating conditions, the measured specific-force direction approximately reveals the gravity direction, allowing roll and pitch drift to be corrected. During dynamic locomotion, however, body acceleration can be large, so accelerometer measurements cannot simply be interpreted as gravity. The estimator must distinguish inertial motion from gravitational effects.

Translational state estimation is more difficult because acceleration must be integrated to obtain velocity and position. Small accelerometer biases become velocity errors and then rapidly growing position errors through repeated integration. Pure inertial navigation is therefore insufficient for sustained quadruped locomotion. Additional information from leg kinematics, contacts, cameras, LiDAR, GNSS, or other sensors is required to bound long-term drift.

Joint encoders provide precise measurements of leg configuration. Combined with a calibrated kinematic model, encoder measurements determine the position of each foot relative to the body. If a stance foot is assumed to remain fixed on the terrain, changes in its body-relative position provide information about body motion relative to the world. This creates a form of leg odometry that complements inertial sensing.

The basic stance-foot assumption states that a securely contacting foot has approximately zero velocity relative to the terrain. Using the leg Jacobian and measured joint velocities, the estimator can calculate foot velocity relative to the body. Combining this quantity with body angular velocity and the zero-foot-velocity constraint provides an observation of body translational velocity that can correct inertial drift.

Contact estimation is therefore inseparable from quadruped state estimation. Applying a zero-velocity constraint to a foot that is actually swinging or slipping introduces severe estimation errors. The estimator must determine which feet provide trustworthy constraints using planned gait phase, estimated ground reaction force, motor torque, joint motion, foot sensors, or probabilistic contact models rather than assuming commanded contact is always correct.

Multiple stance feet provide redundant observations of body motion. During a four-foot stance, several kinematic constraints can simultaneously estimate body velocity and orientation consistency. During trotting, typically fewer constraints are available, while flight phases may temporarily eliminate all kinematic contact observations. Estimation uncertainty should therefore evolve according to the current contact configuration and quality of each supporting foot.

Foot slip is a major source of error in legged odometry. If a slipping foot is incorrectly treated as stationary, the estimator interprets foot motion as body motion and corrupts the state estimate. Slip detection can compare predicted and measured contact behavior, examine inconsistent velocity estimates among stance legs, monitor friction utilization, or combine inertial and visual information to identify unreliable contact constraints.

Sensor fusion combines complementary measurements according to their strengths and uncertainty. IMU data provide high-frequency motion propagation, while kinematic contact observations provide drift correction whenever reliable stance contacts exist. Exteroceptive sensors can provide additional global or local constraints. A well-designed estimator therefore separates rapid state propagation from slower measurement corrections rather than depending on a single sensing modality.

The extended Kalman filter, or EKF, is widely used for quadruped state estimation. The filter propagates a state and covariance using an inertial motion model, then updates them when kinematic or external measurements become available. The covariance represents uncertainty and determines how strongly new measurements influence the estimate. Proper noise modeling is essential because overconfident assumptions can make the filter inconsistent or unstable.

Error-state Kalman filtering is particularly suitable for inertial navigation because orientation errors can be represented locally while the nominal orientation remains on the nonlinear rotation manifold. The estimator propagates the nominal position, velocity, orientation, and sensor biases while maintaining a smaller error state for uncertainty correction. This structure is commonly used when accurate high-rate IMU integration is required.

The estimated state often includes gyroscope and accelerometer biases because these quantities change slowly and strongly influence integrated motion. If the estimator can observe sufficient motion and contact constraints, it can continuously refine bias estimates during operation. Bias estimation reduces long-term drift, although some components may become weakly observable depending on robot motion, terrain, and available measurements.

Observability describes whether unknown state variables can be inferred from the available measurements and motion. Reliable stance contacts constrain velocity strongly, but absolute global position and yaw may remain unobservable without external references. Gravity provides roll and pitch information but does not define global heading. Understanding these limitations prevents the estimator from claiming certainty in state components that sensors cannot physically determine.

The world, body, IMU, hip, and foot coordinate frames must be defined consistently. IMU measurements are initially expressed in the sensor frame and must be transformed using calibrated sensor-to-body extrinsics. Joint kinematics similarly depend on accurate hip locations and link geometry. Small frame or sign errors can produce state-estimation failures that resemble controller instability, making coordinate conventions a critical implementation concern.

Time synchronization is equally important because state estimation combines measurements produced at different rates. IMU samples may arrive at hundreds or thousands of hertz, while joint encoders, force sensors, cameras, and LiDAR operate at different frequencies and delays. Measurements must be associated with accurate timestamps, and estimators may require buffering, interpolation, or delayed updates to avoid interpreting timing errors as physical motion.

Kinematic calibration directly affects leg-odometry accuracy. Errors in joint zero positions, link lengths, joint-axis orientation, or hip mounting locations create systematic errors in computed foot positions and velocities. Because these errors can be repeatedly injected during every stance phase, even small calibration inaccuracies may produce significant drift. Accurate mechanical parameters and encoder calibration are therefore part of the estimation system.

IMU calibration includes estimation of bias, scale factor, axis alignment, and sensor-to-body orientation. Temperature can change bias significantly, particularly during warm-up or prolonged high-load operation. Practical systems may use factory calibration, startup procedures, online bias estimation, and temperature compensation together. Rigid mechanical mounting is also necessary because vibration or structural motion can contaminate inertial measurements.

Legged locomotion produces substantial vibration and impact signals. Foot touchdown generates high-frequency acceleration that may temporarily dominate the IMU measurement, while motor and gearbox vibration can introduce additional noise. Filtering is necessary, but excessive filtering adds phase delay and removes useful dynamic information. Filter bandwidth must therefore be selected according to sensor characteristics and control-loop requirements.

External perception can extend proprioceptive state estimation. Visual-inertial odometry uses cameras and IMU measurements, while LiDAR-inertial odometry uses geometric scan alignment together with inertial propagation. These methods provide environmental references that reduce position and yaw drift when leg contacts are uncertain. They are especially valuable during slippery terrain, jumping, or other conditions where foot-based odometry becomes unreliable.

GNSS can provide global position information for outdoor quadrupeds, and real-time kinematic GNSS can achieve much higher accuracy under suitable satellite visibility. However, buildings, vegetation, tunnels, and indoor environments can degrade or eliminate satellite positioning. A robust architecture therefore treats GNSS as one possible measurement source rather than the sole foundation of state estimation.

Terrain information can also improve estimation by constraining foot height or surface orientation. If a reliable elevation map indicates where a stance foot should contact the environment, the estimator can compare predicted and observed foot geometry. Such constraints can reduce vertical drift, although incorrect terrain maps can introduce systematic errors. Measurement confidence should therefore reflect map quality and local terrain uncertainty.

State estimation must provide more than a best-value estimate to advanced controllers. Uncertainty information can influence foothold selection, velocity limits, and safety decisions. When contact confidence decreases or external localization is lost, the robot may reduce speed or select more conservative gaits. Estimation quality can therefore become an explicit input to locomotion and mission-level decision making.

Estimator failure detection is essential because an incorrect state can rapidly destabilize a quadruped. Innovation residuals, covariance growth, disagreement among sensors, impossible body velocities, and inconsistent contact observations can indicate failure. The system may reject faulty measurements, reset selected states, switch sensing modes, reduce locomotion aggressiveness, or execute a controlled stop when state confidence becomes insufficient.

Simulation and recorded-data replay are valuable for estimator development because identical sensor sequences can be processed repeatedly while algorithms and noise parameters are changed. Ground-truth trajectories from motion capture, high-quality localization, or simulation allow quantitative evaluation of orientation, velocity, and position errors. Testing should include impacts, slip, contact transitions, sensor dropout, bias changes, and aggressive motion.

State estimation ultimately forms the feedback foundation of quadruped locomotion. The IMU supplies rapid inertial information, leg kinematics converts stance contacts into motion constraints, and contact reasoning determines when those constraints are trustworthy. By combining calibrated models, synchronized sensing, probabilistic fusion, bias estimation, slip handling, and external references, the robot can maintain a sufficiently accurate representation of its motion for stable physical control.

사족보행 로봇의 상태 추정(State Estimation)은 불완전한 센서 측정값으로부터 로봇의 몸체 방향, 위치, 속도, 관절 구성 및 접촉 상태를 복원하는 과정이다. 보행 제어기(Locomotion Controller)는 전체 물리 상태를 직접 관측할 수 없으므로 신뢰성 높은 상태 추정값이 필수적이다. 바퀴형 로봇과 달리 사족보행 로봇은 지지 접촉을 반복적으로 변경하기 때문에 상태 추정은 다리 운동학(Leg Kinematics) 및 접촉 판단(Contact Reasoning)과 강하게 결합된다.

관성측정장치(Inertial Measurement Unit, IMU)는 몸체 운동을 추정하기 위한 핵심 센서이다. 일반적인 관성측정장치는 3축 자이로스코프(Gyroscope)와 가속도계(Accelerometer)를 포함하며 일부 시스템은 자기계(Magnetometer)를 추가로 사용한다. 자이로스코프는 각속도를 측정하고 가속도계는 순수한 병진 가속도가 아니라 비력(Specific Force)을 측정한다. 이러한 측정값은 높은 주파수의 운동 정보를 제공하지만 바이어스(Bias), 잡음, 스케일 오차 및 온도 의존적 영향을 포함한다.

몸체 방향(Body Orientation)은 측정된 각속도를 적분하여 전파할 수 있다. 사족보행 로봇은 보행이나 자세 복구 과정에서 큰 롤(Roll), 피치(Pitch), 요(Yaw) 운동을 경험할 수 있으므로 회전 행렬(Rotation Matrix)이나 단위 쿼터니언(Unit Quaternion)이 일반적으로 사용된다. 자이로스코프 적분은 단기적인 방향 추적에는 매우 우수하지만 작은 각속도 바이어스도 시간이 지나면서 누적되어 추가적인 관측값이 제공되지 않으면 방향 드리프트(Orientation Drift)를 발생시킨다.

가속도계는 중력에 대한 방향을 제한하는 데 활용할 수 있는 정보를 제공한다. 정지 상태 또는 가속도가 작은 조건에서는 측정된 비력의 방향으로부터 중력 방향을 근사적으로 추정할 수 있으므로 롤과 피치의 드리프트를 보정할 수 있다. 그러나 동적 보행(Dynamic Locomotion)에서는 몸체 가속도가 크게 발생할 수 있으므로 가속도계 측정값을 단순히 중력으로 해석할 수 없다. 상태 추정기는 관성 운동과 중력 효과를 구분해야 한다.

병진 상태 추정(Translational State Estimation)은 가속도를 적분하여 속도와 위치를 구해야 하기 때문에 더욱 어렵다. 작은 가속도계 바이어스는 속도 오차로 변하고 반복적인 적분을 통해 빠르게 증가하는 위치 오차로 이어진다. 따라서 순수 관성항법(Pure Inertial Navigation)만으로는 지속적인 사족보행에 충분하지 않다. 장기적인 드리프트를 제한하려면 다리 운동학, 접촉, 카메라, 라이다(LiDAR), 위성항법시스템(GNSS) 또는 다른 센서의 추가 정보가 필요하다.

관절 인코더(Joint Encoder)는 다리 구성에 대한 정밀한 측정값을 제공한다. 보정된 운동학 모델(Kinematic Model)과 인코더 측정값을 결합하면 몸체에 대한 각 발의 상대 위치를 계산할 수 있다. 스탠스 발(Stance Foot)이 지형에 고정되어 있다고 가정하면 몸체에 대한 발의 상대 위치 변화로부터 세계 좌표계에 대한 몸체 운동 정보를 얻을 수 있다. 이는 관성 센싱(Inertial Sensing)을 보완하는 다리 오도메트리(Leg Odometry)의 한 형태를 구성한다.

기본적인 스탠스 발 가정은 안정적으로 접촉하고 있는 발의 지형에 대한 속도가 거의 0이라는 것이다. 다리 자코비안(Leg Jacobian)과 측정된 관절 속도를 이용하면 상태 추정기는 몸체에 대한 발의 상대 속도를 계산할 수 있다. 이 값에 몸체 각속도와 발의 영속도 제약조건(Zero-Foot-Velocity Constraint)을 결합하면 몸체 병진 속도에 대한 관측값을 얻을 수 있으며 이를 이용하여 관성 드리프트를 보정할 수 있다.

따라서 접촉 추정(Contact Estimation)은 사족보행 로봇의 상태 추정과 분리할 수 없다. 실제로 스윙하거나 미끄러지고 있는 발에 영속도 제약조건을 적용하면 심각한 상태 추정 오차가 발생한다. 상태 추정기는 명령된 접촉이 항상 정확하다고 가정하기보다 계획된 보행 위상, 추정된 지면 반력(Ground Reaction Force), 모터 토크, 관절 운동, 발 센서 또는 확률적 접촉 모델(Probabilistic Contact Model)을 이용하여 어떤 발이 신뢰할 수 있는 구속조건을 제공하는지 판단해야 한다.

여러 개의 스탠스 발은 몸체 운동에 대한 중복 관측(Redundant Observation)을 제공한다. 네 발이 모두 지면에 접촉한 상태에서는 여러 운동학적 제약조건을 동시에 이용하여 몸체 속도와 방향의 일관성을 추정할 수 있다. 트로팅(Trotting)에서는 일반적으로 사용할 수 있는 제약조건이 감소하며 비행 단계(Flight Phase)에서는 모든 운동학적 접촉 관측이 일시적으로 사라질 수 있다. 따라서 추정 불확실성은 현재 접촉 구성과 각 지지 발의 신뢰도에 따라 변화해야 한다.

발 미끄러짐(Foot Slip)은 다리 오도메트리에서 발생하는 주요 오차 원인이다. 미끄러지는 발을 잘못하여 고정된 것으로 처리하면 상태 추정기는 발의 움직임을 몸체 움직임으로 해석하여 상태 추정값을 왜곡한다. 미끄러짐 감지(Slip Detection)는 예측된 접촉 거동과 측정된 접촉 거동을 비교하거나, 스탠스 다리 사이에서 서로 일치하지 않는 속도 추정값을 검사하거나, 마찰 활용도(Friction Utilization)를 감시하거나, 관성 정보와 시각 정보를 결합하여 신뢰할 수 없는 접촉 제약조건을 식별할 수 있다.

센서 융합(Sensor Fusion)은 서로 다른 측정값의 장점과 불확실성을 고려하여 상호 보완적인 정보를 결합한다. 관성측정장치 데이터는 고주파 운동 전파(Motion Propagation)를 제공하고, 운동학적 접촉 관측은 신뢰할 수 있는 스탠스 접촉이 존재할 때 드리프트를 보정한다. 외수용성 센서(Exteroceptive Sensor)는 추가적인 전역 또는 지역 제약조건을 제공할 수 있다. 따라서 잘 설계된 상태 추정기는 하나의 센싱 방식에 의존하지 않고 빠른 상태 전파와 상대적으로 느린 측정 보정을 분리한다.

확장 칼만 필터(Extended Kalman Filter, EKF)는 사족보행 로봇의 상태 추정에 널리 사용된다. 필터는 관성 운동 모델(Inertial Motion Model)을 사용하여 상태와 공분산(Covariance)을 전파한 후 운동학적 또는 외부 측정값이 제공되면 이를 갱신한다. 공분산은 불확실성을 나타내며 새로운 측정값이 추정 결과에 어느 정도 영향을 줄 것인지를 결정한다. 지나치게 확신하는 가정은 필터의 일관성을 손상시키거나 불안정하게 만들 수 있으므로 적절한 잡음 모델링(Noise Modeling)이 중요하다.

오차 상태 칼만 필터(Error-State Kalman Filter)는 기준 방향을 비선형 회전 다양체(Nonlinear Rotation Manifold)에 유지하면서 방향 오차를 국부적으로 표현할 수 있기 때문에 관성항법에 특히 적합하다. 상태 추정기는 기준 위치, 속도, 방향 및 센서 바이어스를 전파하는 동시에 불확실성 보정을 위한 상대적으로 작은 오차 상태(Error State)를 유지한다. 이러한 구조는 정확한 고주파 관성측정장치 적분이 필요한 경우에 널리 사용된다.

추정 상태에는 일반적으로 자이로스코프와 가속도계의 바이어스도 포함된다. 이러한 값은 천천히 변화하지만 적분된 운동에 큰 영향을 미치기 때문이다. 상태 추정기가 충분한 운동 정보와 접촉 제약조건을 관측할 수 있다면 운용 중에도 바이어스 추정값을 지속적으로 개선할 수 있다. 바이어스 추정은 장기적인 드리프트를 감소시키지만 일부 성분은 로봇 운동, 지형 및 사용 가능한 측정값에 따라 관측 가능성(Observability)이 낮아질 수 있다.

관측 가능성(Observability)은 사용 가능한 측정값과 운동으로부터 알려지지 않은 상태 변수를 추론할 수 있는지를 나타낸다. 신뢰성 높은 스탠스 접촉은 속도를 강하게 제한하지만 외부 기준이 없으면 절대 전역 위치와 요 방향은 관측되지 않을 수 있다. 중력은 롤과 피치에 대한 정보를 제공하지만 전역 진행 방향(Global Heading)은 정의하지 않는다. 이러한 한계를 이해하면 센서가 물리적으로 결정할 수 없는 상태 성분에 대해 상태 추정기가 잘못된 확신을 갖는 것을 방지할 수 있다.

세계 좌표계(World Frame), 몸체 좌표계(Body Frame), 관성측정장치 좌표계(IMU Frame), 고관절 좌표계(Hip Frame), 발 좌표계(Foot Frame)는 일관되게 정의되어야 한다. 관성측정장치의 측정값은 처음에는 센서 좌표계에서 표현되며 보정된 센서-몸체 외부 파라미터(Sensor-to-Body Extrinsics)를 이용하여 변환해야 한다. 관절 운동학도 정확한 고관절 위치와 링크 형상에 의존한다. 작은 좌표계 또는 부호 오류도 제어기 불안정성과 유사한 상태 추정 실패를 발생시킬 수 있으므로 좌표 규약(Coordinate Convention)은 구현에서 매우 중요하다.

상태 추정은 서로 다른 주기로 생성되는 측정값을 결합하기 때문에 시간 동기화(Time Synchronization)도 중요하다. 관성측정장치 샘플은 수백 또는 수천 헤르츠로 제공될 수 있지만 관절 인코더, 힘 센서, 카메라 및 라이다는 서로 다른 주파수와 지연시간으로 동작한다. 측정값에는 정확한 타임스탬프(Timestamp)가 연결되어야 하며 상태 추정기는 타이밍 오차를 실제 물리 운동으로 잘못 해석하지 않도록 버퍼링(Buffering), 보간(Interpolation) 또는 지연 갱신(Delayed Update)을 사용할 수 있다.

운동학적 보정(Kinematic Calibration)은 다리 오도메트리의 정확도에 직접적인 영향을 준다. 관절 영점 위치, 링크 길이, 관절축 방향 또는 고관절 장착 위치의 오차는 계산된 발 위치와 속도에 체계적인 오차를 발생시킨다. 이러한 오차는 모든 스탠스 단계에서 반복적으로 주입될 수 있으므로 작은 보정 오차도 상당한 드리프트를 발생시킬 수 있다. 따라서 정확한 기계 파라미터와 인코더 보정은 상태 추정 시스템의 일부로 다루어야 한다.

관성측정장치 보정(IMU Calibration)에는 바이어스, 스케일 계수(Scale Factor), 축 정렬(Axis Alignment), 센서-몸체 방향의 추정이 포함된다. 온도는 특히 초기 워밍업 또는 장시간 고부하 운용 중에 바이어스를 크게 변화시킬 수 있다. 실제 시스템에서는 공장 보정, 시동 절차, 온라인 바이어스 추정 및 온도 보상을 함께 사용할 수 있다. 진동이나 구조적 운동이 관성 측정값을 오염시키지 않도록 견고한 기계적 장착도 필요하다.

다리형 보행은 상당한 진동과 충격 신호를 발생시킨다. 발 착지는 고주파 가속도를 발생시켜 일시적으로 관성측정장치 측정값을 지배할 수 있으며 모터와 기어박스의 진동도 추가적인 잡음을 발생시킬 수 있다. 필터링(Filtering)이 필요하지만 지나친 필터링은 위상 지연(Phase Delay)을 증가시키고 유용한 동적 정보를 제거한다. 따라서 필터 대역폭(Filter Bandwidth)은 센서 특성과 제어 루프 요구조건을 고려하여 선정해야 한다.

외부 환경 인식(External Perception)은 고유수용성 상태 추정(Proprioceptive State Estimation)을 확장할 수 있다. 시각-관성 오도메트리(Visual-Inertial Odometry)는 카메라와 관성측정장치 측정값을 사용하고, 라이다-관성 오도메트리(LiDAR-Inertial Odometry)는 기하학적 스캔 정합(Scan Alignment)과 관성 상태 전파를 결합한다. 이러한 방법은 다리 접촉이 불확실할 때 위치 및 요 방향 드리프트를 감소시키는 환경 기준을 제공한다. 특히 미끄러운 지형, 점프 또는 발 기반 오도메트리의 신뢰성이 낮아지는 상황에서 유용하다.

위성항법시스템(Global Navigation Satellite System, GNSS)은 실외 사족보행 로봇에 전역 위치 정보를 제공할 수 있으며, 적절한 위성 가시성이 확보되면 실시간 이동측위(Real-Time Kinematic, RTK) GNSS를 통해 훨씬 높은 정확도를 얻을 수 있다. 그러나 건물, 식생, 터널 및 실내 환경은 위성 위치추정 성능을 저하시키거나 완전히 사용할 수 없게 만들 수 있다. 따라서 강건한 아키텍처에서는 GNSS를 상태 추정의 유일한 기반이 아니라 여러 가능한 측정 소스 중 하나로 취급한다.

지형 정보(Terrain Information)는 발 높이 또는 표면 방향을 제한함으로써 상태 추정을 개선할 수도 있다. 신뢰할 수 있는 고도 지도(Elevation Map)가 스탠스 발이 환경의 어느 위치와 접촉해야 하는지를 나타낸다면 상태 추정기는 예측된 발 형상과 관측된 발 형상을 비교할 수 있다. 이러한 제약조건은 수직 방향 드리프트를 감소시킬 수 있지만 잘못된 지형 지도는 체계적인 오차를 발생시킬 수 있다. 따라서 측정 신뢰도는 지도 품질과 지역 지형의 불확실성을 반영해야 한다.

상태 추정은 고급 제어기에 단순한 최적 추정값만 제공해서는 안 된다. 불확실성 정보(Uncertainty Information)는 발 디딤 위치 선택, 속도 제한 및 안전 의사결정에 영향을 줄 수 있다. 접촉 신뢰도가 감소하거나 외부 위치추정 기능이 상실되면 로봇은 속도를 줄이거나 보다 보수적인 보행 패턴을 선택할 수 있다. 따라서 상태 추정 품질은 보행 및 임무 수준 의사결정의 명시적인 입력으로 활용될 수 있다.

잘못된 상태 정보는 사족보행 로봇을 매우 빠르게 불안정하게 만들 수 있으므로 상태 추정기 고장 감지(Estimator Failure Detection)가 필수적이다. 이노베이션 잔차(Innovation Residual), 공분산 증가, 센서 사이의 불일치, 물리적으로 불가능한 몸체 속도 및 일관되지 않은 접촉 관측은 고장을 나타낼 수 있다. 시스템은 잘못된 측정값을 거부하거나 특정 상태를 재설정하고, 센싱 모드를 전환하거나, 보행의 공격성을 낮추거나, 상태 신뢰도가 충분하지 않을 경우 제어된 정지를 수행할 수 있다.

시뮬레이션(Simulation)과 기록 데이터 재생(Recorded-Data Replay)은 동일한 센서 시퀀스를 반복적으로 처리하면서 알고리즘과 잡음 파라미터를 변경할 수 있기 때문에 상태 추정기 개발에 유용하다. 모션 캡처(Motion Capture), 고정밀 위치추정 또는 시뮬레이션으로부터 얻은 실측 기준 궤적(Ground-Truth Trajectory)을 이용하면 방향, 속도 및 위치 오차를 정량적으로 평가할 수 있다. 시험에는 충격, 미끄러짐, 접촉 전환, 센서 누락, 바이어스 변화 및 공격적인 운동 조건이 포함되어야 한다.

상태 추정은 궁극적으로 사족보행 로봇 보행의 피드백 기반(Feedback Foundation)을 형성한다. 관성측정장치는 빠른 관성 정보를 제공하고, 다리 운동학은 스탠스 접촉을 운동 제약조건으로 변환하며, 접촉 판단은 이러한 제약조건을 언제 신뢰할 수 있는지를 결정한다. 보정된 모델, 동기화된 센싱, 확률적 융합(Probabilistic Fusion), 바이어스 추정, 미끄러짐 처리 및 외부 기준 정보를 결합함으로써 로봇은 안정적인 물리적 제어에 충분히 정확한 자신의 운동 상태 표현을 유지할 수 있다.

##  

## 01.08. Quadruped Safety E Stop Posture Recovery [w/Code]

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

Quadruped robot safety must address hazards created by high-torque actuators, dynamic locomotion, unstable body configurations, environmental uncertainty, and failures in sensing or computation. Unlike a stationary industrial robot, a quadruped can fall, slide, collide, or continue moving after losing balance. Safety architecture must therefore coordinate hardware protection, real-time supervision, emergency stopping, controlled posture transitions, and recovery behavior.

Safety should be designed as multiple independent layers rather than as a single software function. Local actuator protection handles current, temperature, voltage, velocity, and joint limits, while locomotion supervision evaluates body state, contacts, and controller health. Higher-level safety monitors navigation and mission behavior. Independent emergency mechanisms provide a final path for removing or restricting actuator power when normal control can no longer guarantee safe behavior.

A safety state machine provides a structured representation of robot operating conditions. Typical states may include power-off, initialization, stand-ready, active locomotion, degraded operation, controlled stop, emergency stop, fallen state, and recovery. Transitions should depend on explicit conditions and verified system health rather than informal software flags. This structure prevents incompatible commands from reaching actuators during abnormal conditions.

Emergency stop, or E-stop, is intended to bring the system toward a safe condition when continued operation presents unacceptable risk. It should not be treated as an ordinary pause command. Depending on mechanical design and operating context, an E-stop may disable torque immediately, command a controlled reduction of torque, activate braking mechanisms, or transition through a dedicated safe-stop sequence before power removal.

Immediate torque removal is not always mechanically safe for a legged robot. A standing quadruped can collapse when joint torque disappears, potentially creating additional impact or crushing hazards. For this reason, the safety design must distinguish between emergency power interruption and controlled stopping. When sufficient control authority remains, the robot may first reduce velocity and lower its body before actuator torque is removed or restricted.

A controlled stop is appropriate when a fault is detected but the control system remains functional. Desired body velocity can be reduced toward zero, swing legs can complete safe touchdown, and ground reaction forces can be redistributed among available stance legs. The robot can then transition toward a stable standing, crouching, or sitting posture. This reduces kinetic energy and produces a more predictable final configuration.

The E-stop signal path should minimize dependence on complex high-level software. A physical emergency-stop device can be connected through a dedicated safety circuit, safety controller, or hardware interlock capable of overriding ordinary motion commands. Software may report the event and coordinate shutdown, but the fundamental stop function should not depend entirely on perception, navigation, artificial intelligence, or non-real-time middleware remaining operational.

Remote emergency stopping is important when quadrupeds operate at distance from personnel or in hazardous environments. Wireless stop mechanisms must consider communication loss, latency, interference, and authentication. Loss of a required safety heartbeat can trigger a predefined safe response. However, wireless communication should not be assumed perfectly reliable, so local onboard supervision remains necessary even when remote operators are present.

Watchdog mechanisms detect failures in processors, control loops, communication links, and software processes. A real-time watchdog can verify that torque-control or locomotion loops execute within expected deadlines, while communication watchdogs detect stale commands or missing sensor updates. If a critical heartbeat disappears, the system should enter a predetermined degraded or safe state instead of continuing indefinitely with outdated information.

Joint-level protection provides the first defense against damaging actuator behavior. Position, velocity, torque, current, and temperature limits should be enforced close to the actuator interface. Soft limits can gradually reduce commands as joints approach boundaries, while hard limits provide final protection against excessive motion. Mechanical stops may offer additional protection, but repeated high-energy impacts against them should never be considered normal control behavior.

Command validation prevents invalid references from propagating into low-level controllers. Joint commands can be checked for numerical validity, rate of change, magnitude, and consistency with actuator capabilities. Whole-body commands can similarly be checked against feasible body orientation, height, velocity, and contact conditions. NaN values, communication corruption, or sudden discontinuities should be rejected before they generate physical motion.

Body-state monitoring is essential because individual actuators can remain within their limits while the overall robot becomes unsafe. Roll, pitch, body height, angular velocity, linear velocity, and estimated support conditions can be compared with operating envelopes. Large orientation errors or rapid angular motion may indicate an imminent fall. Safety logic can then reduce commanded motion, modify stance, or transition to a protective posture.

Contact information provides another safety indicator. Unexpected loss of a stance contact, repeated foot slip, excessive impact, or disagreement between commanded and measured contact can indicate unstable terrain or controller failure. Rather than waiting for body orientation to exceed a critical threshold, the system can respond early by widening support, reducing speed, lowering the center of mass, or stopping locomotion.

Fall detection combines body orientation, angular velocity, body height, contact state, and sometimes impact measurements. A robot should distinguish a temporary aggressive maneuver from an unrecoverable fall. Simple angle thresholds alone may generate false triggers during dynamic locomotion. Combining several state variables with persistence conditions allows the system to determine whether active balancing remains feasible or a protective response should begin.

When a fall becomes unavoidable, the objective changes from maintaining nominal locomotion to minimizing damage. The controller may reduce leg extension, avoid violent corrective torques, and move limbs toward configurations that protect joints, sensors, payloads, and surrounding objects. The appropriate protective posture depends on robot morphology because vulnerable cameras, LiDAR units, manipulators, batteries, and joint structures occupy different locations.

Posture control provides safe transitions between standing, crouching, sitting, lying, and other predefined configurations. These transitions should be generated as controlled motions rather than abrupt joint-position changes. Joint limits, self-collision, center-of-mass motion, contact conditions, and actuator torque capacity must remain satisfied. Slow posture transitions are often useful during startup, shutdown, maintenance, and fault handling.

A safe standing posture should provide adequate support margin while avoiding actuator saturation. Body height and leg configuration influence both stability and joint loading. Excessively extended legs can reduce disturbance tolerance, whereas extremely crouched configurations may require large continuous torques. Safety postures should therefore be selected using both geometric stability and actuator thermal or mechanical constraints.

Posture recovery refers to restoring a controllable configuration after the robot has fallen or entered an abnormal pose. Recovery may begin from the side, back, front, or partially collapsed configurations. Before attempting motion, the robot should estimate its orientation, joint configuration, available clearance, actuator condition, and environmental constraints. Recovery should not automatically begin when nearby obstacles or people make the motion unsafe.

Self-righting motions often require large joint excursions and significant transient torque. The robot may use coordinated leg movement to rotate the body, create support points, shift the center of mass, and eventually place the feet beneath the body. Recovery trajectories must respect self-collision and joint limits while avoiding repeated impacts. Torque and velocity limits may differ from those used during normal locomotion.

Recovery can be organized as a sequence of posture states rather than one complex motion. The controller first classifies the fallen orientation, selects an appropriate recovery strategy, moves toward an intermediate configuration, establishes stable contacts, and then raises the body. State transitions can be verified using orientation and contact feedback. This structure makes recovery easier to test and prevents blind execution of an open-loop motion.

Recovery failure must itself be handled safely. A blocked leg, slippery floor, damaged actuator, insufficient battery voltage, or unexpected obstacle can prevent completion of the sequence. The controller should limit the number or duration of recovery attempts and monitor progress. Repeatedly applying maximum torque without meaningful motion can overheat actuators or damage the mechanism and should trigger a safe abort condition.

Actuator thermal state remains important during safety and recovery behavior. Holding a crouched posture or repeatedly attempting self-righting can demand high current for extended periods. Temperature estimates and current limits should therefore remain active even when normal locomotion limits are temporarily modified. A safety behavior that protects the robot from falling but overheats the actuators is not a complete safety solution.

Battery and power-system monitoring also participates in safe locomotion. Low state of charge, excessive current, undervoltage, overvoltage, or abnormal battery temperature can reduce available actuator capability. A sudden reduction in power during dynamic locomotion may cause a fall. Energy-related warnings should therefore trigger progressively conservative behavior, allowing the robot to stop or assume a stable posture before power becomes insufficient.

Sensor-health monitoring is necessary because safety decisions depend on state information. Invalid IMU data, encoder disagreement, force-sensor faults, timestamp errors, or localization failures can make normal control unsafe. Redundant or cross-checked measurements can help identify failures. When critical sensing becomes unavailable, the robot should reduce its operating envelope or enter a state that requires fewer assumptions about environmental and body state.

Safety supervision should remain separated from learning-based or high-level autonomous decision making. Reinforcement-learning policies, foundation models, or mission planners may propose actions, but their outputs should pass through deterministic constraints and safety monitors before reaching actuators. This allows advanced autonomy to operate within a defined physical envelope while independent mechanisms retain authority to limit or reject unsafe commands.

Restarting after an E-stop requires controlled reinitialization rather than immediate restoration of previous commands. The system should verify actuator communication, sensor health, body orientation, contact state, and command sources before torque is re-enabled. Previous velocity or trajectory commands should normally be cleared. The robot can then enter a known posture or stand-ready state before autonomous operation resumes.

Safety events should be logged with synchronized state information so that failures can be reconstructed. E-stop activation, watchdog timeout, excessive joint torque, fall detection, slip events, thermal limits, recovery attempts, and controller transitions should be recorded together with relevant sensor and command data. Such records support root-cause analysis, regression testing, maintenance, and improvement of safety thresholds.

Simulation provides an efficient environment for testing abnormal conditions before physical experiments. Communication loss, actuator faults, sensor corruption, extreme body orientation, low friction, unexpected contact loss, and recovery failure can be injected repeatedly. Simulation cannot replace hardware validation, but it allows dangerous corner cases to be explored systematically before exposing the physical robot or nearby personnel to them.

Physical safety validation should progress from constrained tests to increasingly realistic operation. Emergency stopping, controlled lowering, fall detection, protective posture, self-righting, watchdog behavior, and actuator limiting should be verified individually before being combined with dynamic locomotion. Test procedures should evaluate not only whether a safety function activates, but also whether the resulting physical motion actually reduces risk.

Quadruped safety is therefore an integrated property of mechanical design, electronics, real-time control, state estimation, locomotion software, and operational procedures. E-stop mechanisms provide a final intervention path, while continuous supervision attempts to prevent conditions from reaching that point. Posture control and recovery extend safety beyond stopping by giving the robot structured methods for reaching or restoring mechanically stable configurations.

A robust safety architecture treats normal locomotion, fault response, emergency stopping, protective behavior, and recovery as parts of one coordinated state framework. The objective is not merely to stop software execution but to manage the physical energy and configuration of the robot. By combining independent protection layers, deterministic limits, reliable fault detection, controlled posture transitions, and validated recovery strategies, a quadruped can operate with substantially greater physical reliability.

사족보행 로봇 안전(Quadruped Robot Safety)은 고토크 액추에이터(High-Torque Actuator), 동적 보행(Dynamic Locomotion), 불안정한 몸체 구성, 환경 불확실성 및 센싱이나 계산 시스템의 고장으로 발생할 수 있는 위험을 다루어야 한다. 고정된 산업용 로봇과 달리 사족보행 로봇은 균형을 잃은 후 넘어지거나, 미끄러지거나, 충돌하거나, 계속 움직일 수 있다. 따라서 안전 아키텍처(Safety Architecture)는 하드웨어 보호, 실시간 감독, 비상 정지, 제어된 자세 전환 및 복구 동작을 통합적으로 조정해야 한다.

안전은 하나의 소프트웨어 기능으로 구현하기보다 여러 개의 독립적인 계층(Independent Layer)으로 설계해야 한다. 로컬 액추에이터 보호(Local Actuator Protection)는 전류, 온도, 전압, 속도 및 관절 제한을 처리하고, 보행 감독(Locomotion Supervision)은 몸체 상태, 접촉 및 제어기 건전성을 평가한다. 상위 안전 기능은 내비게이션과 임무 동작을 감시한다. 독립적인 비상 메커니즘은 정상적인 제어가 더 이상 안전한 동작을 보장할 수 없을 때 액추에이터 전력을 제거하거나 제한하기 위한 최종 경로를 제공한다.

안전 상태 머신(Safety State Machine)은 로봇의 운용 조건을 구조적으로 표현한다. 일반적인 상태에는 전원 차단(Power-Off), 초기화(Initialization), 기립 준비(Stand-Ready), 능동 보행(Active Locomotion), 성능 제한 운용(Degraded Operation), 제어 정지(Controlled Stop), 비상 정지(Emergency Stop), 전도 상태(Fallen State), 복구(Recovery) 등이 포함될 수 있다. 상태 전환은 비공식적인 소프트웨어 플래그가 아니라 명시적인 조건과 검증된 시스템 건전성에 따라 결정되어야 한다. 이러한 구조는 비정상 상태에서 서로 양립할 수 없는 명령이 액추에이터로 전달되는 것을 방지한다.

비상 정지(Emergency Stop, E-Stop)는 동작을 계속하는 것이 허용할 수 없는 위험을 발생시키는 경우 시스템을 안전한 상태로 전환하기 위한 기능이다. 비상 정지는 일반적인 일시 정지 명령(Pause Command)으로 취급해서는 안 된다. 기계 설계와 운용 환경에 따라 비상 정지는 즉시 토크를 비활성화하거나, 제어된 방식으로 토크를 감소시키거나, 제동 메커니즘을 작동시키거나, 전력을 차단하기 전에 전용 안전 정지 시퀀스(Safe-Stop Sequence)를 수행할 수 있다.

즉각적인 토크 제거(Immediate Torque Removal)가 다리형 로봇에서 항상 기계적으로 안전한 것은 아니다. 서 있는 사족보행 로봇은 관절 토크가 사라지면 붕괴할 수 있으며, 이로 인해 추가적인 충격이나 압착 위험(Crushing Hazard)이 발생할 수 있다. 따라서 안전 설계에서는 비상 전원 차단(Emergency Power Interruption)과 제어 정지(Controlled Stop)를 구분해야 한다. 충분한 제어 권한이 남아 있다면 로봇은 액추에이터 토크를 제거하거나 제한하기 전에 먼저 속도를 줄이고 몸체를 낮출 수 있다.

제어 정지는 고장이 감지되었지만 제어 시스템이 여전히 정상적으로 기능할 수 있을 때 적합하다. 목표 몸체 속도를 점진적으로 0으로 줄이고, 스윙 다리(Swing Leg)가 안전하게 착지하도록 하며, 사용 가능한 스탠스 다리(Stance Leg) 사이에 지면 반력(Ground Reaction Force)을 재분배할 수 있다. 이후 로봇은 안정적인 기립, 웅크림(Crouching) 또는 앉은 자세로 전환할 수 있다. 이를 통해 운동 에너지(Kinetic Energy)를 감소시키고 보다 예측 가능한 최종 구성을 만들 수 있다.

비상 정지 신호 경로(E-Stop Signal Path)는 복잡한 상위 수준 소프트웨어에 대한 의존성을 최소화해야 한다. 물리적 비상 정지 장치(Physical Emergency-Stop Device)는 일반적인 운동 명령을 무시할 수 있는 전용 안전 회로, 안전 제어기(Safety Controller) 또는 하드웨어 인터록(Hardware Interlock)에 연결할 수 있다. 소프트웨어는 이벤트를 보고하고 종료 절차를 조정할 수 있지만 기본적인 정지 기능은 인식, 내비게이션, 인공지능 또는 비실시간 미들웨어가 계속 정상적으로 동작하는 것에 전적으로 의존해서는 안 된다.

원격 비상 정지(Remote Emergency Stop)는 사족보행 로봇이 작업자로부터 떨어져 있거나 위험한 환경에서 운용될 때 중요하다. 무선 정지 메커니즘(Wireless Stop Mechanism)은 통신 손실, 지연시간, 간섭 및 인증(Authentication)을 고려해야 한다. 필요한 안전 하트비트(Safety Heartbeat)가 손실되면 사전에 정의된 안전 대응을 실행할 수 있다. 그러나 무선 통신을 완벽하게 신뢰할 수 있다고 가정해서는 안 되므로 원격 작업자가 존재하더라도 로봇 내부의 온보드 감독(Onboard Supervision)이 필요하다.

워치독 메커니즘(Watchdog Mechanism)은 프로세서, 제어 루프, 통신 링크 및 소프트웨어 프로세스의 고장을 감지한다. 실시간 워치독(Real-Time Watchdog)은 토크 제어 또는 보행 제어 루프가 예상된 시간 제한 내에서 실행되는지를 검증할 수 있으며, 통신 워치독은 오래된 명령이나 센서 갱신 손실을 감지한다. 중요한 하트비트가 사라지면 시스템은 오래된 정보를 사용하여 무기한 동작을 계속하는 대신 사전에 정의된 성능 제한 상태 또는 안전 상태로 전환해야 한다.

관절 수준 보호(Joint-Level Protection)는 액추에이터의 위험한 동작을 방지하기 위한 첫 번째 방어 계층을 제공한다. 위치, 속도, 토크, 전류 및 온도 제한은 액추에이터 인터페이스에 가까운 위치에서 적용되어야 한다. 소프트 제한(Soft Limit)은 관절이 경계에 가까워짐에 따라 명령을 점진적으로 감소시킬 수 있으며, 하드 제한(Hard Limit)은 과도한 움직임에 대한 최종 보호를 제공한다. 기계적 스토퍼(Mechanical Stop)는 추가적인 보호를 제공할 수 있지만 높은 에너지로 반복 충돌하는 상황을 정상적인 제어 방식으로 간주해서는 안 된다.

명령 검증(Command Validation)은 유효하지 않은 기준 명령이 저수준 제어기로 전달되는 것을 방지한다. 관절 명령은 수치적 유효성, 변화율, 크기 및 액추에이터 성능과의 일관성을 검사할 수 있다. 전신 명령(Whole-Body Command)도 실행 가능한 몸체 방향, 높이, 속도 및 접촉 조건과 비교하여 검사할 수 있다. 숫자가 아닌 값(Not a Number, NaN), 통신 데이터 손상 또는 갑작스러운 불연속 명령은 실제 물리적 움직임을 발생시키기 전에 거부되어야 한다.

몸체 상태 감시(Body-State Monitoring)는 개별 액추에이터가 제한 범위 안에 있더라도 전체 로봇이 위험한 상태에 도달할 수 있기 때문에 필수적이다. 롤(Roll), 피치(Pitch), 몸체 높이, 각속도, 선속도 및 추정된 지지 상태를 운용 허용 영역(Operating Envelope)과 비교할 수 있다. 큰 자세 오차 또는 빠른 각운동은 임박한 전도(Imminent Fall)를 나타낼 수 있다. 이 경우 안전 로직은 명령된 움직임을 감소시키거나, 스탠스를 수정하거나, 보호 자세로 전환할 수 있다.

접촉 정보(Contact Information)는 또 다른 안전 지표를 제공한다. 예상하지 못한 스탠스 접촉의 상실, 반복적인 발 미끄러짐, 과도한 충격 또는 명령된 접촉과 측정된 접촉 사이의 불일치는 불안정한 지형이나 제어기 고장을 나타낼 수 있다. 몸체 방향이 임계값을 초과할 때까지 기다리는 대신 시스템은 지지 영역을 넓히고, 속도를 감소시키며, 무게중심(Center of Mass)을 낮추거나, 보행을 정지시키는 방식으로 조기에 대응할 수 있다.

전도 감지(Fall Detection)는 몸체 방향, 각속도, 몸체 높이, 접촉 상태 및 경우에 따라 충격 측정값을 결합한다. 로봇은 일시적인 공격적 기동(Aggressive Maneuver)과 복구 불가능한 전도를 구분할 수 있어야 한다. 단순한 각도 임계값만 사용하면 동적 보행 중 잘못된 감지가 발생할 수 있다. 여러 상태 변수와 지속시간 조건(Persistence Condition)을 결합하면 능동 균형 제어가 여전히 가능한지 또는 보호 대응을 시작해야 하는지를 판단할 수 있다.

전도를 더 이상 피할 수 없게 되면 제어 목표는 정상 보행 유지에서 손상 최소화로 변경된다. 제어기는 다리의 신장을 줄이고, 과도한 보정 토크를 피하며, 관절, 센서, 탑재물 및 주변 물체를 보호할 수 있는 구성으로 다리를 이동시킬 수 있다. 적절한 보호 자세(Protective Posture)는 로봇의 형태에 따라 달라지는데, 취약한 카메라, 라이다(LiDAR), 매니퓰레이터(Manipulator), 배터리 및 관절 구조물이 서로 다른 위치에 배치되기 때문이다.

자세 제어(Posture Control)는 기립, 웅크림, 앉기, 눕기 및 기타 사전에 정의된 자세 사이의 안전한 전환을 제공한다. 이러한 전환은 갑작스러운 관절 위치 변경이 아니라 제어된 움직임으로 생성되어야 한다. 관절 제한, 자체 충돌(Self-Collision), 무게중심 운동, 접촉 조건 및 액추에이터 토크 성능을 지속적으로 만족해야 한다. 느린 자세 전환은 시동, 종료, 유지보수 및 고장 처리 과정에서 특히 유용하다.

안전 기립 자세(Safe Standing Posture)는 액추에이터 포화를 방지하면서 충분한 지지 여유(Support Margin)를 제공해야 한다. 몸체 높이와 다리 구성은 안정성과 관절 하중 모두에 영향을 준다. 지나치게 신장된 다리는 외란에 대한 허용도를 감소시킬 수 있으며, 지나치게 웅크린 구성은 큰 연속 토크를 요구할 수 있다. 따라서 안전 자세는 기하학적 안정성과 액추에이터의 열적 또는 기계적 제약을 함께 고려하여 선정해야 한다.

자세 복구(Posture Recovery)는 로봇이 넘어지거나 비정상적인 자세에 진입한 이후 다시 제어 가능한 구성으로 복원하는 것을 의미한다. 복구는 옆으로 누운 상태, 등을 대고 누운 상태, 전면으로 넘어진 상태 또는 부분적으로 붕괴된 상태에서 시작될 수 있다. 동작을 시도하기 전에 로봇은 자신의 방향, 관절 구성, 사용 가능한 주변 공간, 액추에이터 상태 및 환경 제약조건을 추정해야 한다. 주변 장애물이나 사람이 복구 동작을 위험하게 만들 수 있다면 자동으로 복구를 시작해서는 안 된다.

자가 기립 동작(Self-Righting Motion)은 일반적으로 큰 관절 운동 범위와 상당한 과도 토크(Transient Torque)를 요구한다. 로봇은 여러 다리의 움직임을 조정하여 몸체를 회전시키고, 지지점을 형성하며, 무게중심을 이동시킨 후 최종적으로 발을 몸체 아래에 배치할 수 있다. 복구 궤적(Recovery Trajectory)은 자체 충돌과 관절 제한을 만족하면서 반복적인 충격을 방지해야 한다. 토크와 속도 제한은 정상 보행에서 사용하는 값과 다르게 설정될 수도 있다.

복구는 하나의 복잡한 움직임보다 여러 자세 상태(Posture State)의 시퀀스로 구성할 수 있다. 제어기는 먼저 전도 방향을 분류하고 적절한 복구 전략을 선택한 후 중간 구성으로 이동하고, 안정적인 접촉을 형성한 다음 몸체를 들어 올린다. 상태 전환은 방향 및 접촉 피드백을 사용하여 검증할 수 있다. 이러한 구조는 복구 동작의 시험을 쉽게 하고 개방 루프 운동(Open-Loop Motion)을 맹목적으로 실행하는 것을 방지한다.

복구 실패(Recovery Failure) 자체도 안전하게 처리해야 한다. 움직일 수 없는 다리, 미끄러운 바닥, 손상된 액추에이터, 부족한 배터리 전압 또는 예상하지 못한 장애물은 복구 시퀀스의 완료를 방해할 수 있다. 제어기는 복구 시도의 횟수 또는 지속시간을 제한하고 진행 상태를 감시해야 한다. 의미 있는 움직임 없이 최대 토크를 반복적으로 가하면 액추에이터가 과열되거나 기구가 손상될 수 있으므로 안전 중단 조건(Safe Abort Condition)을 실행해야 한다.

액추에이터 열 상태(Actuator Thermal State)는 안전 및 복구 동작에서도 중요하다. 웅크린 자세를 유지하거나 자가 기립을 반복적으로 시도하면 장시간 높은 전류가 요구될 수 있다. 따라서 정상 보행 제한이 일시적으로 수정되는 경우에도 온도 추정과 전류 제한은 계속 활성화되어야 한다. 로봇의 전도는 방지하지만 액추에이터를 과열시키는 안전 동작은 완전한 안전 솔루션이라고 할 수 없다.

배터리 및 전력 시스템 감시(Battery and Power-System Monitoring)도 안전한 보행에 관여한다. 낮은 충전 상태(State of Charge), 과도한 전류, 저전압, 과전압 또는 비정상적인 배터리 온도는 사용 가능한 액추에이터 성능을 감소시킬 수 있다. 동적 보행 중 갑작스럽게 전력이 감소하면 로봇이 넘어질 수 있다. 따라서 에너지 관련 경고는 단계적으로 보수적인 동작을 실행하여 전력이 부족해지기 전에 로봇이 정지하거나 안정적인 자세를 취하도록 해야 한다.

안전 의사결정은 상태 정보에 의존하므로 센서 건전성 감시(Sensor-Health Monitoring)가 필요하다. 유효하지 않은 관성측정장치(IMU) 데이터, 인코더 불일치, 힘 센서 고장, 타임스탬프 오류 또는 위치 추정 실패는 정상 제어를 위험하게 만들 수 있다. 중복 측정 또는 교차 검증(Cross-Checking)은 고장을 식별하는 데 도움이 된다. 중요한 센싱 기능을 사용할 수 없게 되면 로봇은 운용 영역을 축소하거나 환경과 몸체 상태에 대한 가정을 적게 요구하는 상태로 전환해야 한다.

안전 감독(Safety Supervision)은 학습 기반 또는 상위 수준 자율 의사결정과 분리된 상태로 유지되어야 한다. 강화학습 정책(Reinforcement-Learning Policy), 파운데이션 모델(Foundation Model) 또는 임무 플래너(Mission Planner)가 동작을 제안할 수 있지만 해당 출력은 액추에이터에 전달되기 전에 결정론적 제약조건과 안전 감시기를 통과해야 한다. 이를 통해 고급 자율 기능은 정의된 물리적 운용 영역 안에서 동작하고 독립적인 메커니즘은 위험한 명령을 제한하거나 거부할 권한을 유지할 수 있다.

비상 정지 이후 재시작(Restart)은 이전 명령을 즉시 복원하는 것이 아니라 제어된 재초기화(Controlled Reinitialization)를 통해 수행해야 한다. 시스템은 토크를 다시 활성화하기 전에 액추에이터 통신, 센서 건전성, 몸체 방향, 접촉 상태 및 명령 소스를 검증해야 한다. 이전의 속도 또는 궤적 명령은 일반적으로 삭제해야 한다. 이후 로봇은 자율 운용을 다시 시작하기 전에 알려진 자세 또는 기립 준비 상태로 진입할 수 있다.

안전 이벤트(Safety Event)는 고장 상황을 재구성할 수 있도록 동기화된 상태 정보와 함께 기록해야 한다. 비상 정지 작동, 워치독 타임아웃(Watchdog Timeout), 과도한 관절 토크, 전도 감지, 미끄러짐 이벤트, 열 제한, 복구 시도 및 제어기 상태 전환을 관련 센서 및 명령 데이터와 함께 기록해야 한다. 이러한 기록은 근본 원인 분석(Root-Cause Analysis), 회귀 시험(Regression Testing), 유지보수 및 안전 임계값 개선을 지원한다.

시뮬레이션(Simulation)은 실제 하드웨어 시험 전에 비정상적인 조건을 검증하기 위한 효율적인 환경을 제공한다. 통신 손실, 액추에이터 고장, 센서 데이터 손상, 극단적인 몸체 방향, 낮은 마찰, 예상하지 못한 접촉 상실 및 복구 실패를 반복적으로 주입할 수 있다. 시뮬레이션이 실제 하드웨어 검증을 대체할 수는 없지만 물리적 로봇이나 주변 작업자를 위험에 노출시키기 전에 위험한 경계 조건(Corner Case)을 체계적으로 탐색할 수 있다.

물리적 안전 검증(Physical Safety Validation)은 제한된 시험에서 시작하여 점진적으로 실제 운용 조건에 가까운 환경으로 확장해야 한다. 비상 정지, 제어된 몸체 하강, 전도 감지, 보호 자세, 자가 기립, 워치독 동작 및 액추에이터 제한 기능을 동적 보행과 통합하기 전에 각각 독립적으로 검증해야 한다. 시험 절차에서는 안전 기능이 단순히 활성화되는지만 평가하는 것이 아니라 그 결과 발생하는 물리적 움직임이 실제로 위험을 감소시키는지도 평가해야 한다.

따라서 사족보행 로봇 안전은 기계 설계, 전자장치, 실시간 제어, 상태 추정, 보행 소프트웨어 및 운용 절차가 통합된 시스템 특성(System Property)이다. 비상 정지 메커니즘은 최종적인 개입 경로를 제공하고 지속적인 안전 감독은 상황이 그 단계까지 진행되는 것을 방지하려고 한다. 자세 제어와 복구는 로봇이 기계적으로 안정된 구성에 도달하거나 이를 다시 복원할 수 있는 구조화된 방법을 제공함으로써 단순한 정지를 넘어 안전 기능을 확장한다.

강건한 안전 아키텍처(Robust Safety Architecture)는 정상 보행, 고장 대응, 비상 정지, 보호 동작 및 복구를 하나의 통합된 상태 프레임워크(State Framework)의 일부로 다룬다. 목표는 단순히 소프트웨어 실행을 중지하는 것이 아니라 로봇의 물리적 에너지와 구성을 관리하는 것이다. 독립적인 보호 계층, 결정론적 제한, 신뢰성 높은 고장 감지, 제어된 자세 전환 및 검증된 복구 전략을 결합함으로써 사족보행 로봇의 물리적 신뢰성을 크게 향상시킬 수 있다.

##  

## 01.09. Platform Survey Spot ANYmal Aliengo B2 A1

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

Commercial quadruped platforms demonstrate how common principles of legged locomotion are implemented under different requirements for mobility, payload, autonomy, durability, and research accessibility. Boston Dynamics Spot, ANYbotics ANYmal, Unitree Aliengo, B2, and A1 represent several important design directions, ranging from industrial inspection robots to research-oriented and cost-conscious platforms. Comparing them reveals how hardware and software choices reflect intended operating environments.

Boston Dynamics Spot is designed as a general-purpose mobile robotic platform for industrial inspection, remote operation, sensing, and autonomous missions. Its four articulated legs allow movement through environments containing stairs, uneven surfaces, narrow passages, and obstacles that challenge conventional wheeled robots. The platform emphasizes integrated mobility rather than exposing every low-level locomotion mechanism directly to application developers.

Spot illustrates a product-oriented quadruped architecture in which locomotion, state estimation, balance, and many safety functions are integrated into the platform. Users can focus on mission-level behaviors, payload sensing, inspection workflows, and autonomy through supported interfaces. This approach reduces the engineering effort required to deploy a legged robot, although it provides a different development experience from platforms intended primarily for low-level locomotion research.

A major characteristic of Spot is its support for modular payload integration. Cameras, environmental sensors, communication devices, computational modules, and inspection equipment can be mounted according to application requirements. This makes the robot useful as a mobile sensing platform in industrial facilities. Payload integration, however, must consider mass, center-of-mass location, power consumption, communication interfaces, and the influence of added equipment on mobility.

ANYmal, developed by ANYbotics, represents another major industrial quadruped design direction. The platform has been developed around autonomous inspection and operation in complex industrial environments where stairs, narrow spaces, rough surfaces, and infrastructure obstacles are common. Its architecture emphasizes robust locomotion, environmental perception, autonomous navigation, mission execution, and integration of inspection sensors into a field-deployable robotic system.

ANYmal is particularly significant because its development history connects advanced academic legged-robot research with commercial industrial deployment. Research on dynamic locomotion, state estimation, terrain adaptation, whole-body control, and autonomous navigation contributed to the broader technical foundation associated with the platform. This makes ANYmal an important example of how algorithms developed in research environments can evolve toward reliable operation under practical industrial constraints.

Industrial quadrupeds such as Spot and ANYmal must address requirements extending far beyond the ability to demonstrate dynamic walking. Reliability, environmental protection, communication robustness, battery management, autonomous mission execution, inspection repeatability, and safe behavior around infrastructure become central design concerns. Consequently, commercial performance should not be evaluated only through maximum speed or visually impressive locomotion maneuvers.

Unitree Aliengo represents a different balance between performance, development accessibility, and platform cost. It has been widely recognized as a quadruped platform suitable for research, education, algorithm development, and experimental applications. Its conventional four-leg morphology and electrically actuated joints provide a practical system for studying locomotion control, perception, navigation, reinforcement learning, and integration of external computing or sensing systems.

Aliengo can be viewed as part of the transition from expensive specialized quadruped prototypes toward more accessible commercial legged robots. This transition is important because algorithm research requires repeated physical experimentation. When platforms become easier to acquire and operate, researchers can evaluate gait generation, state estimation, terrain perception, mapping, navigation, and learned control on real hardware rather than relying exclusively on simulation.

Unitree A1 further illustrates the importance of compact and relatively accessible quadruped hardware for research. A1 became widely used in academic demonstrations and experimental projects involving reinforcement learning, sim-to-real transfer, locomotion control, perception, and autonomous navigation. Its significance is therefore not limited to its mechanical specifications; it also lies in the ecosystem of research methods and software experiments that developed around compact commercial quadrupeds.

A1 is smaller and lighter than heavy industrial quadrupeds, which affects both capability and experimental practicality. Lower platform mass can simplify transportation and laboratory testing, while smaller actuators and structure naturally limit payload and some operating conditions. These tradeoffs demonstrate that robot size is not simply a scaling parameter. Mass, actuator capability, leg inertia, battery capacity, structural strength, and achievable contact forces interact throughout the design.

Unitree B2 represents a substantially heavier-duty direction than compact platforms such as A1. It targets demanding mobility and industrial applications requiring greater payload capability, stronger environmental performance, and operation over challenging terrain. A larger platform can carry more substantial sensing or application equipment, but increased mass also raises actuator torque requirements, impact energy, structural loads, battery demands, and safety considerations during operation.

The contrast between A1 and B2 demonstrates how quadruped design changes when the target mission shifts from laboratory experimentation toward industrial transportation or inspection. A compact robot can prioritize portability, development convenience, and lower experimental risk, while a larger industrial platform must emphasize structural robustness, sustained mobility, payload support, thermal management, and protection against environmental exposure.

Despite their differences, these platforms share a broadly similar mechanical organization. Four articulated legs are distributed around a central body containing batteries, computing hardware, communication electronics, and supporting systems. Each leg typically provides multiple actuated degrees of freedom that allow the foot to move through a three-dimensional workspace. Coordinated control of twelve or more actuated joints enables body stabilization and terrain-adaptive stepping.

Actuator design strongly influences the behavior of every platform. High torque density enables compact joints, while low reflected inertia and suitable transmission characteristics improve dynamic response and interaction with terrain. Industrial systems additionally require durability, sealing, thermal management, and long service life. Research-oriented systems may place greater emphasis on control accessibility and rapid experimentation, although mechanical robustness remains essential for repeated locomotion testing.

State estimation is another common architectural requirement. IMU measurements, joint encoders, contact information, and kinematic models provide the basic proprioceptive estimate required for balance and locomotion. Depending on the platform and application, cameras, depth sensors, LiDAR, or other localization systems can extend this estimate. Reliable state estimation is fundamental because the controller must continuously determine body orientation, velocity, and contact condition while the support pattern changes.

Terrain perception distinguishes autonomous field operation from basic blind locomotion. Industrial platforms commonly integrate environmental sensing so that the robot can identify obstacles, stairs, surfaces, passages, and traversable regions. Research platforms can be equipped with similar sensors, but the perception stack may be developed by the user. This difference reflects a broader distinction between purchasing a deployable robotic capability and purchasing hardware for algorithm development.

Software accessibility is therefore an important comparison dimension. A highly integrated commercial robot may provide stable application programming interfaces for navigation, payload control, mission execution, and data acquisition while keeping safety-critical locomotion functions internally managed. A research-oriented platform may expose lower-level commands and state information, allowing greater experimentation with controllers but transferring more responsibility for stability and safety to the developer.

The intended payload also changes the role of the quadruped. An inspection robot may carry thermal cameras, acoustic sensors, gas detectors, high-resolution imaging systems, or industrial communication equipment. A research robot may instead carry a GPU computer, depth camera, LiDAR, or experimental sensor package. Payload mass alone is insufficient for evaluation because mounting position changes the center of mass and therefore affects balance and actuator loading.

Mobility performance should be interpreted through terrain capability rather than speed alone. Stair climbing, slope traversal, obstacle negotiation, operation on loose or irregular ground, turning in constrained areas, and recovery from disturbances may be more important than maximum forward velocity. A robot intended for industrial inspection must repeatedly complete missions under uncertain conditions rather than merely demonstrate a short high-speed maneuver.

Battery endurance is similarly application dependent. A compact research robot may be acceptable with relatively short experiments followed by battery replacement or charging. Industrial inspection requires useful mission duration, predictable energy consumption, safe battery management, and integration with operational workflows. Autonomous docking or charging can become important when robots are expected to execute repeated missions without continuous human intervention.

Environmental robustness creates another major distinction among platforms. Laboratory robots can operate on controlled floors and under supervised conditions, whereas industrial quadrupeds may encounter dust, water, temperature variation, outdoor surfaces, vibration, and communication degradation. Mechanical sealing, connector selection, sensor protection, thermal design, and fault handling therefore become part of the locomotion system\'s practical capability.

Safety requirements also scale with robot mass and mission context. A small research quadruped can still cause injury, but a large platform carries substantially greater kinetic and gravitational energy. Emergency stopping, velocity limits, collision avoidance, actuator protection, communication-loss behavior, controlled posture transitions, and operator procedures become increasingly important as robot size, payload, and autonomy increase.

The platforms also demonstrate different approaches to autonomy. Teleoperation can provide direct human supervision, while waypoint navigation and autonomous mission execution reduce operator workload. Industrial deployment increasingly requires the robot to repeat inspection routes, respond to obstacles, collect sensor data, and return results without continuous manual control. Autonomy therefore combines locomotion with mapping, localization, planning, perception, and mission management.

For researchers selecting a quadruped, the best platform depends on the experimental objective rather than a single performance ranking. Low-level locomotion research benefits from accessible actuator commands, state feedback, simulation support, and software flexibility. Industrial autonomy research may prioritize payload integration, perception sensors, reliability, and navigation interfaces. Heavy-load applications require greater structural and actuator capability even if this increases cost and operational complexity.

Spot and ANYmal illustrate highly integrated industrial robotic systems where locomotion is part of a broader autonomous inspection capability. Aliengo and A1 illustrate the value of comparatively accessible platforms for experimentation and algorithm development. B2 extends the Unitree family toward heavier-duty mobility and industrial operation. These categories overlap, but they provide useful reference points for understanding how product requirements shape quadruped architecture.

A platform survey should therefore avoid comparing robots only through isolated specification values. Payload, speed, runtime, mass, sensing, environmental protection, software interfaces, autonomy, actuator accessibility, safety architecture, and application ecosystem must be considered together. Published specifications can also vary by hardware generation and configuration, so detailed engineering selection should always use the documentation corresponding to the exact model and revision being evaluated.

Taken together, Spot, ANYmal, Aliengo, B2, and A1 demonstrate the maturation of quadruped robotics from specialized dynamic machines into a diverse platform class. Their differences show that there is no universally optimal quadruped configuration. Successful design emerges from matching morphology, actuators, sensing, computing, software abstraction, safety, payload capability, and autonomy to the intended physical task and operating environment.

상용 사족보행 로봇 플랫폼(Commercial Quadruped Platform)은 다리형 보행(Legged Locomotion)의 공통 원리가 이동성, 탑재 능력, 자율성, 내구성 및 연구 접근성에 대한 서로 다른 요구조건에 따라 어떻게 구현되는지를 보여준다. 보스턴 다이내믹스 스팟(Boston Dynamics Spot), 애니보틱스 애니멀(ANYbotics ANYmal), 유니트리 Aliengo, B2 및 A1은 산업용 검사 로봇부터 연구 지향적이고 비용 접근성이 높은 플랫폼까지 여러 중요한 설계 방향을 대표한다. 이들을 비교하면 하드웨어와 소프트웨어 선택이 목표 운용 환경을 어떻게 반영하는지 이해할 수 있다.

보스턴 다이내믹스 스팟(Boston Dynamics Spot)은 산업 검사, 원격 운용, 센싱 및 자율 임무를 위한 범용 이동 로봇 플랫폼(General-Purpose Mobile Robotic Platform)으로 설계되었다. 네 개의 관절형 다리를 이용하여 일반적인 바퀴형 로봇이 이동하기 어려운 계단, 불규칙한 표면, 좁은 통로 및 장애물이 존재하는 환경을 이동할 수 있다. 이 플랫폼은 응용 개발자가 모든 저수준 보행 메커니즘을 직접 다루도록 하기보다는 통합된 이동성(Integrated Mobility)을 제공하는 데 중점을 둔다.

스팟은 보행, 상태 추정(State Estimation), 균형 제어 및 다양한 안전 기능이 플랫폼 내부에 통합된 제품 지향형 사족보행 아키텍처(Product-Oriented Quadruped Architecture)를 보여준다. 사용자는 지원되는 인터페이스를 통해 임무 수준 동작, 탑재 센싱, 검사 작업 흐름 및 자율 기능에 집중할 수 있다. 이러한 접근법은 다리형 로봇을 배치하는 데 필요한 엔지니어링 작업을 줄여주지만 저수준 보행 연구를 주요 목적으로 하는 플랫폼과는 다른 개발 경험을 제공한다.

스팟의 주요 특징 중 하나는 모듈식 탑재장치 통합(Modular Payload Integration)을 지원한다는 것이다. 카메라, 환경 센서, 통신 장치, 컴퓨팅 모듈 및 검사 장비를 응용 요구조건에 따라 장착할 수 있다. 이를 통해 산업 시설에서 이동형 센싱 플랫폼(Mobile Sensing Platform)으로 활용할 수 있다. 그러나 탑재장치 통합에서는 질량, 무게중심 위치, 전력 소비, 통신 인터페이스 및 추가 장비가 이동성에 미치는 영향을 고려해야 한다.

애니보틱스(ANYbotics)가 개발한 애니멀(ANYmal)은 또 다른 주요 산업용 사족보행 설계 방향을 대표한다. 이 플랫폼은 계단, 좁은 공간, 거친 표면 및 설비 장애물이 흔히 존재하는 복잡한 산업 환경에서 자율 검사와 운용을 수행하도록 개발되었다. 아키텍처는 강건한 보행(Robust Locomotion), 환경 인식, 자율 내비게이션, 임무 수행 및 검사 센서를 현장 배치 가능한 로봇 시스템(Field-Deployable Robotic System)에 통합하는 데 중점을 둔다.

애니멀은 첨단 학술 다리형 로봇 연구와 상업적 산업 배치를 연결해 온 개발 이력 때문에 특히 중요하다. 동적 보행, 상태 추정, 지형 적응(Terrain Adaptation), 전신 제어(Whole-Body Control) 및 자율 내비게이션에 관한 연구는 이 플랫폼과 관련된 광범위한 기술적 기반에 기여했다. 따라서 애니멀은 연구 환경에서 개발된 알고리즘이 실제 산업적 제약조건 아래에서 신뢰성 있게 운용되는 시스템으로 어떻게 발전할 수 있는지를 보여주는 중요한 사례이다.

스팟과 애니멀 같은 산업용 사족보행 로봇은 동적 보행을 시연할 수 있는 능력을 훨씬 넘어서는 요구조건을 충족해야 한다. 신뢰성, 환경 보호(Environmental Protection), 통신 강건성, 배터리 관리, 자율 임무 수행, 검사 반복성 및 산업 설비 주변에서의 안전한 동작이 핵심 설계 요소가 된다. 따라서 상용 플랫폼의 성능은 최대 속도나 시각적으로 인상적인 보행 동작만으로 평가해서는 안 된다.

유니트리 Aliengo는 성능, 개발 접근성 및 플랫폼 비용 사이에서 다른 균형점을 보여준다. Aliengo는 연구, 교육, 알고리즘 개발 및 실험적 응용에 적합한 사족보행 플랫폼으로 널리 활용되어 왔다. 일반적인 네 다리 형태와 전기식 관절 액추에이터를 갖추고 있어 보행 제어, 인식, 내비게이션, 강화학습(Reinforcement Learning) 및 외부 컴퓨팅 또는 센싱 시스템의 통합을 연구하기 위한 실용적인 시스템을 제공한다.

Aliengo는 고가의 특수 사족보행 시제품에서 보다 접근 가능한 상용 다리형 로봇으로 전환되는 과정의 일부로 볼 수 있다. 이러한 변화는 알고리즘 연구에서 실제 하드웨어를 이용한 반복적인 실험이 필요하다는 점에서 중요하다. 플랫폼을 보다 쉽게 확보하고 운용할 수 있게 되면 연구자는 시뮬레이션에만 의존하지 않고 실제 하드웨어에서 보행 생성, 상태 추정, 지형 인식, 매핑, 내비게이션 및 학습 기반 제어를 평가할 수 있다.

유니트리 A1(Unitree A1)은 연구를 위한 소형이면서 비교적 접근성이 높은 사족보행 하드웨어의 중요성을 더욱 잘 보여준다. A1은 강화학습, 시뮬레이션-실환경 전이(Sim-to-Real Transfer), 보행 제어, 인식 및 자율 내비게이션과 관련된 학술 시연과 실험 프로젝트에서 널리 활용되었다. 따라서 A1의 중요성은 단순한 기계적 사양에만 있는 것이 아니라 소형 상용 사족보행 로봇을 중심으로 발전한 연구 방법과 소프트웨어 실험 생태계에도 있다.

A1은 중대형 산업용 사족보행 로봇보다 작고 가벼우며 이러한 특성은 성능과 실험 편의성 모두에 영향을 준다. 낮은 플랫폼 질량은 운반과 실험실 시험을 용이하게 만들 수 있지만 작은 액추에이터와 구조는 자연스럽게 탑재 능력과 일부 운용 조건을 제한한다. 이러한 절충관계는 로봇의 크기가 단순한 스케일링 파라미터가 아니라는 점을 보여준다. 질량, 액추에이터 성능, 다리 관성, 배터리 용량, 구조 강도 및 생성 가능한 접촉력이 전체 설계에서 상호작용한다.

유니트리 B2(Unitree B2)는 A1과 같은 소형 플랫폼보다 훨씬 중장비 지향적인 설계 방향을 보여준다. B2는 더 높은 탑재 능력, 강한 환경 대응 성능 및 험난한 지형에서의 운용이 필요한 이동성과 산업 응용을 목표로 한다. 더 큰 플랫폼은 보다 대형의 센싱 또는 응용 장비를 운반할 수 있지만 질량 증가로 인해 액추에이터 토크 요구량, 충격 에너지, 구조 하중, 배터리 요구량 및 운용 과정의 안전 문제도 함께 증가한다.

A1과 B2의 차이는 목표 임무가 실험실 연구에서 산업 운송이나 검사로 변화할 때 사족보행 로봇의 설계가 어떻게 달라지는지를 보여준다. 소형 로봇은 이동 편의성, 개발 편의성 및 낮은 실험 위험을 우선할 수 있는 반면 대형 산업 플랫폼은 구조적 강건성, 지속적인 이동 성능, 탑재물 지지, 열관리(Thermal Management) 및 환경 노출에 대한 보호를 강조해야 한다.

이러한 차이에도 불구하고 각 플랫폼은 대체로 유사한 기계적 구성(Mechanical Organization)을 공유한다. 네 개의 관절형 다리가 배터리, 컴퓨팅 하드웨어, 통신 전자장치 및 지원 시스템을 포함하는 중앙 몸체 주변에 배치된다. 각각의 다리는 일반적으로 발이 3차원 작업공간을 이동할 수 있도록 여러 개의 구동 자유도(Actuated Degree of Freedom)를 제공한다. 12개 이상의 구동 관절을 협조 제어함으로써 몸체 안정화와 지형 적응형 스테핑(Terrain-Adaptive Stepping)을 구현할 수 있다.

액추에이터 설계(Actuator Design)는 모든 플랫폼의 동작 특성에 큰 영향을 미친다. 높은 토크 밀도(Torque Density)는 소형 관절 설계를 가능하게 하며 낮은 반사 관성(Reflected Inertia)과 적절한 전달 특성은 동적 응답과 지형 상호작용을 향상시킨다. 산업용 시스템은 추가적으로 내구성, 밀폐성, 열관리 및 긴 사용 수명을 요구한다. 연구 지향형 시스템은 제어 접근성과 빠른 실험을 더욱 중요하게 고려할 수 있지만 반복적인 보행 시험을 위해서는 기계적 강건성 역시 필수적이다.

상태 추정(State Estimation)은 모든 플랫폼에서 공통적으로 요구되는 또 하나의 아키텍처 요소이다. 관성측정장치(IMU), 관절 인코더, 접촉 정보 및 운동학 모델은 균형과 보행에 필요한 기본적인 고유수용성 상태 추정(Proprioceptive State Estimation)을 제공한다. 플랫폼과 응용에 따라 카메라, 깊이 센서, 라이다 또는 다른 위치추정 시스템을 이용하여 이러한 상태 추정을 확장할 수 있다. 지지 패턴이 지속적으로 변화하는 동안 제어기는 몸체 방향, 속도 및 접촉 상태를 계속 판단해야 하므로 신뢰성 높은 상태 추정은 필수적이다.

지형 인식(Terrain Perception)은 자율적인 현장 운용을 기본적인 블라인드 보행(Blind Locomotion)과 구분하는 중요한 요소이다. 산업용 플랫폼은 일반적으로 환경 센싱 기능을 통합하여 장애물, 계단, 표면, 통로 및 이동 가능한 영역을 식별할 수 있도록 한다. 연구용 플랫폼에도 유사한 센서를 장착할 수 있지만 인식 스택(Perception Stack)은 사용자가 직접 개발해야 할 수 있다. 이러한 차이는 배치 가능한 로봇 기능 자체를 구매하는 것과 알고리즘 개발용 하드웨어를 구매하는 것 사이의 보다 근본적인 차이를 반영한다.

따라서 소프트웨어 접근성(Software Accessibility)은 플랫폼을 비교하기 위한 중요한 기준이다. 고도로 통합된 상용 로봇은 안전이 중요한 보행 기능을 내부적으로 관리하면서 내비게이션, 탑재장치 제어, 임무 수행 및 데이터 수집을 위한 안정적인 응용 프로그래밍 인터페이스(Application Programming Interface, API)를 제공할 수 있다. 연구 지향형 플랫폼은 보다 저수준의 명령과 상태 정보에 접근할 수 있도록 하여 제어기 실험의 자유도를 높이는 대신 안정성과 안전에 대한 더 많은 책임을 개발자에게 부여할 수 있다.

목표 탑재장치(Intended Payload) 역시 사족보행 로봇의 역할을 변화시킨다. 검사 로봇은 열화상 카메라, 음향 센서, 가스 검출기, 고해상도 영상 시스템 또는 산업용 통신 장비를 운반할 수 있다. 연구용 로봇은 대신 그래픽처리장치(GPU) 컴퓨터, 깊이 카메라, 라이다 또는 실험용 센서 패키지를 탑재할 수 있다. 탑재물의 질량만으로는 충분한 평가가 되지 않는데, 장착 위치가 무게중심을 변화시키고 결과적으로 균형과 액추에이터 하중에 영향을 주기 때문이다.

이동 성능(Mobility Performance)은 단순히 속도만으로 평가하기보다 지형 대응 능력을 중심으로 해석해야 한다. 계단 등반, 경사면 횡단, 장애물 극복, 느슨하거나 불규칙한 지면에서의 운용, 제한된 공간에서의 회전 및 외란으로부터의 복구 능력은 최대 전진 속도보다 더 중요할 수 있다. 산업 검사 로봇은 짧은 시간 동안 고속 동작을 시연하는 것보다 불확실한 조건에서 반복적으로 임무를 완료할 수 있어야 한다.

배터리 운용시간(Battery Endurance) 역시 응용 분야에 따라 중요성이 달라진다. 소형 연구용 로봇에서는 비교적 짧은 실험 후 배터리를 교체하거나 충전하는 방식이 허용될 수 있다. 반면 산업 검사는 실질적인 임무 수행시간, 예측 가능한 에너지 소비, 안전한 배터리 관리 및 실제 작업 흐름과의 통합을 요구한다. 사람이 지속적으로 개입하지 않고 반복적인 임무를 수행해야 하는 경우 자율 도킹(Autonomous Docking)이나 충전 기능도 중요해질 수 있다.

환경 강건성(Environmental Robustness)은 플랫폼 사이의 또 다른 주요 차이를 형성한다. 실험실 로봇은 통제된 바닥과 감독되는 환경에서 동작할 수 있지만 산업용 사족보행 로봇은 먼지, 물, 온도 변화, 실외 표면, 진동 및 통신 성능 저하를 경험할 수 있다. 따라서 기계적 밀폐(Mechanical Sealing), 커넥터 선정, 센서 보호, 열 설계 및 고장 처리는 보행 시스템의 실질적인 성능을 구성하는 요소가 된다.

안전 요구조건(Safety Requirement) 역시 로봇의 질량과 임무 환경에 따라 증가한다. 소형 연구용 사족보행 로봇도 부상을 발생시킬 수 있지만 대형 플랫폼은 훨씬 큰 운동 에너지와 중력 위치에너지를 가진다. 따라서 로봇의 크기, 탑재물 및 자율성이 증가할수록 비상 정지(Emergency Stop), 속도 제한, 충돌 회피, 액추에이터 보호, 통신 손실 대응, 제어된 자세 전환 및 작업자 운용 절차가 더욱 중요해진다.

이들 플랫폼은 자율성(Autonomy)에 대한 서로 다른 접근법도 보여준다. 원격조작(Teleoperation)은 사람이 직접 감독할 수 있도록 하고, 웨이포인트 내비게이션(Waypoint Navigation)과 자율 임무 수행은 작업자의 부담을 감소시킨다. 산업 현장에서는 로봇이 지속적인 수동 조작 없이 검사 경로를 반복하고, 장애물에 대응하며, 센서 데이터를 수집하고, 결과를 반환할 수 있어야 하는 요구가 증가한다. 따라서 자율성은 보행뿐만 아니라 매핑, 위치추정, 계획, 인식 및 임무 관리를 통합한다.

사족보행 로봇을 선정하는 연구자에게 가장 적합한 플랫폼은 단일 성능 순위가 아니라 실험 목적에 따라 결정된다. 저수준 보행 연구에서는 액추에이터 명령 접근성, 상태 피드백, 시뮬레이션 지원 및 소프트웨어 유연성이 중요하다. 산업 자율성 연구에서는 탑재장치 통합, 인식 센서, 신뢰성 및 내비게이션 인터페이스를 우선할 수 있다. 중량물 운반 응용에서는 비용과 운용 복잡성이 증가하더라도 더 높은 구조적 및 액추에이터 성능이 필요하다.

스팟과 애니멀은 보행 기능이 보다 광범위한 자율 검사 기능의 일부로 통합된 고도화된 산업용 로봇 시스템을 보여준다. Aliengo와 A1은 실험과 알고리즘 개발을 위한 상대적으로 접근성 높은 플랫폼의 가치를 보여준다. B2는 유니트리 제품군을 보다 중장비 지향적인 이동성과 산업 운용 영역으로 확장한다. 이러한 범주는 서로 일부 중첩되지만 제품 요구조건이 사족보행 로봇의 아키텍처를 어떻게 형성하는지 이해하기 위한 유용한 기준점을 제공한다.

따라서 플랫폼 조사(Platform Survey)에서는 개별적인 사양 값만으로 로봇을 비교해서는 안 된다. 탑재 능력, 속도, 운용시간, 질량, 센싱, 환경 보호, 소프트웨어 인터페이스, 자율성, 액추에이터 접근성, 안전 아키텍처 및 응용 생태계를 함께 고려해야 한다. 공개된 사양은 하드웨어 세대와 구성에 따라 달라질 수 있으므로 상세한 엔지니어링 선정 과정에서는 평가 대상이 되는 정확한 모델과 리비전(Revision)에 해당하는 문서를 사용해야 한다.

종합하면 스팟, 애니멀, Aliengo, B2 및 A1은 사족보행 로봇 기술이 특수한 동적 보행 장비에서 다양한 목적을 가진 플랫폼 계열로 성숙해 온 과정을 보여준다. 이들 플랫폼의 차이는 모든 응용에 보편적으로 최적인 사족보행 구성이 존재하지 않는다는 사실을 보여준다. 성공적인 설계는 형태(Morphology), 액추에이터, 센싱, 컴퓨팅, 소프트웨어 추상화, 안전, 탑재 능력 및 자율성을 목표 물리 작업과 운용 환경에 적절하게 결합하는 것에서 이루어진다.

##  

## 01.10. Robotics Quadruped Target Application Scope

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

Defining the target application scope of a quadruped robot is a system-engineering activity that connects mobility technology with real operational requirements. A quadruped should not be developed simply because legged locomotion is technically possible. Its value appears when the environment contains stairs, obstacles, uneven terrain, narrow passages, or discontinuous surfaces that significantly reduce the effectiveness of conventional wheeled platforms.

The application scope begins with the operating environment. Indoor factories, power plants, construction sites, underground facilities, forests, disaster zones, and outdoor infrastructure impose different mobility requirements. Surface geometry, slope, stair dimensions, floor strength, available clearance, lighting, weather, dust, water, temperature, and communication coverage must be characterized before locomotion capability and sensing architecture are selected.

Terrain complexity is one of the strongest reasons for selecting a quadruped architecture. Continuous flat surfaces generally favor wheels because of their mechanical simplicity and energy efficiency. Quadrupeds become advantageous when the robot must cross steps, rubble, gaps, irregular ground, vegetation, steep slopes, or structures designed for human access. The application should therefore justify the additional mechanical and computational complexity of legged mobility.

Industrial inspection is a major target application because many facilities contain stairs, pipes, platforms, narrow corridors, and equipment distributed across multiple elevations. A quadruped can carry cameras, thermal imagers, acoustic sensors, gas detectors, LiDAR, or other inspection instruments while following predefined routes. The primary objective is not merely walking but repeatedly transporting sensing capability to locations where useful measurements must be collected.

Oil, gas, chemical, and energy facilities provide representative inspection environments. Robots may be required to observe gauges, identify thermal anomalies, detect leaks, record equipment sound, inspect structural conditions, and create spatial records. These tasks require integration of locomotion with localization, mapping, mission planning, sensor positioning, data logging, communication, and safe operation around industrial infrastructure.

Power-generation and utility environments create similar requirements but may introduce additional hazards such as restricted areas, electromagnetic interference, heat, water, confined passages, or hazardous equipment. A quadruped can reduce routine human exposure by performing repetitive inspection routes. However, practical deployment requires predictable mission completion, reliable fault handling, and the ability to return to a safe location when sensing, localization, communication, or power becomes degraded.

Construction-site monitoring is another suitable application because the environment changes continuously and often lacks smooth navigation surfaces. A quadruped can traverse temporary ramps, unfinished floors, stairs, debris, and uneven ground while collecting images or three-dimensional mapping data. Repeated surveys can support progress monitoring, dimensional comparison, safety inspection, and documentation of site conditions as construction evolves.

Underground mines, tunnels, and subterranean infrastructure present difficult combinations of rough terrain, limited satellite positioning, dust, darkness, communication constraints, and potentially hazardous conditions. Quadrupeds can provide mobile sensing where wheeled robots may have difficulty maintaining traction or negotiating obstacles. Such applications place strong requirements on local state estimation, LiDAR or visual localization, terrain perception, communication resilience, and autonomous recovery behavior.

Search-and-rescue and disaster-response environments represent a more demanding application class. Collapsed structures, debris, unstable surfaces, narrow openings, poor visibility, and uncertain maps can make conventional mobility difficult. A quadruped may transport cameras, microphones, environmental sensors, communication relays, or lightweight supplies into areas that are dangerous for personnel, but reliability and operator awareness become critical because terrain conditions can exceed normal locomotion assumptions.

Forest, agricultural, and natural-terrain applications emphasize adaptation to irregular and deformable surfaces. Grass, roots, rocks, soil, mud, slopes, and vegetation produce contact conditions that differ significantly from laboratory floors. Successful operation requires robust contact estimation, slip handling, terrain-aware foothold selection, and perception capable of identifying both geometric and mechanical hazards rather than treating every visually clear region as safely traversable.

Security and patrol applications can use quadrupeds to repeat routes through facilities that contain stairs or mixed indoor-outdoor terrain. The robot may carry visual, thermal, acoustic, or environmental sensors and report anomalies to remote operators. In this role, mobility is only one part of the system. Long-duration autonomy, charging, fleet management, communication security, event detection, human supervision, and predictable safety behavior determine operational usefulness.

Remote telepresence is another application category in which the quadruped acts as a mobile embodiment for a distant operator. Cameras, microphones, speakers, and environmental sensors allow the operator to inspect locations and interact with personnel without being physically present. Legged mobility extends telepresence beyond smooth office environments into industrial spaces, outdoor infrastructure, and complex facilities containing stairs or uneven surfaces.

Payload transportation can be considered when materials, tools, sensors, or supplies must move through terrain unsuitable for conventional carts or autonomous mobile robots. The application must define payload mass, center-of-mass variation, required speed, travel distance, terrain severity, and loading method. Carrying capacity cannot be considered independently because additional payload directly changes joint torque, contact force, energy consumption, stability margin, and thermal loading.

A quadruped equipped with a robotic arm extends mobility into loco-manipulation. Instead of only observing equipment, the robot may operate a door, turn a valve, press a button, manipulate a handle, pick up an object, or position a sensor close to a target. These tasks couple manipulation forces with balance and locomotion, requiring coordinated whole-body control rather than treating the arm and mobile base as independent robotic systems.

Inspection manipulation is particularly valuable when a sensor must be positioned precisely. A body-mounted camera may be unable to observe a gauge hidden behind equipment, whereas an articulated arm can move the sensor to an appropriate viewpoint. The same principle applies to contact probes, microphones, thermal sensors, or maintenance tools. The quadruped then functions as a mobile manipulation platform rather than only as a walking sensor carrier.

The target scope should distinguish autonomous operation from teleoperation. Teleoperation can reduce autonomy requirements but increases dependence on communication quality and operator skill. Autonomous missions require localization, terrain understanding, path planning, obstacle avoidance, locomotion adaptation, failure detection, and recovery. Many practical systems combine both approaches, allowing autonomous execution under normal conditions and human intervention when uncertainty becomes excessive.

Operational range is determined by more than battery capacity. Energy consumption changes with terrain, gait, payload, speed, temperature, and repeated posture transitions. Mission planning must reserve sufficient energy for returning to a charging or recovery location. Industrial deployment may additionally require automatic docking or battery management so that repeated missions can be executed without continuous manual servicing.

The application scope should explicitly define expected locomotion capability. Requirements may include walking speed, minimum passage width, maximum slope, stair geometry, obstacle height, ground clearance, turning radius, allowable foot slip, and recovery capability. These requirements can then be translated into leg workspace, actuator torque, body dimensions, gait selection, perception range, and controller performance rather than relying on vague objectives such as good rough-terrain mobility.

Environmental protection must also follow the application. Indoor laboratory operation requires relatively little protection, while field deployment may require resistance to rain, dust, mud, vibration, temperature variation, and accidental impact. Sensor windows, joints, connectors, batteries, computers, and cooling paths must remain functional under expected conditions. Environmental robustness therefore affects mechanical design, electronics, software monitoring, and maintenance procedures simultaneously.

Communication requirements depend on the level of autonomy and operational risk. A teleoperated robot may require continuous low-latency communication, while a highly autonomous robot can continue its mission through temporary network interruptions. Safety-critical commands such as stop requests require particularly reliable handling. The system should define behavior for reduced bandwidth, packet loss, complete communication loss, and restoration of the network connection.

Human interaction must be considered whenever quadrupeds operate around workers or the public. Operators should be able to understand robot state, mission intention, faults, and safety status. Speed restrictions, exclusion zones, audible or visual indicators, emergency-stop mechanisms, and predictable stopping behavior may be required. A technically capable locomotion system is not operationally acceptable if nearby personnel cannot anticipate or safely respond to its behavior.

The application scope also determines the appropriate level of artificial intelligence. Learning-based locomotion can improve terrain adaptation, while semantic perception can identify meaningful objects and regions. Vision-language or foundation-model components may support mission interpretation and human interaction. These functions should complement rather than bypass deterministic safety, state estimation, motion constraints, and low-level control required for reliable physical operation.

Multi-robot deployment introduces another application dimension. Several quadrupeds can divide inspection areas, share maps, relay communication, or provide redundant coverage. Fleet operation requires task allocation, mission scheduling, map consistency, charging coordination, health monitoring, and recovery procedures. The benefit of additional robots should therefore be evaluated at the system level rather than assuming that duplicating individual autonomous robots automatically produces effective cooperation.

Application selection should consider alternatives to quadruped mobility. Wheeled autonomous mobile robots, tracked vehicles, drones, fixed sensors, or conventional human inspection may solve some tasks more economically. A quadruped is justified when its ability to negotiate human-oriented or irregular environments creates sufficient operational value to offset greater cost, energy consumption, maintenance complexity, and control requirements.

A practical target application should therefore be expressed as a measurable operational scenario rather than a general statement such as inspection or patrol. The scenario should specify environment, terrain, mission duration, payload, sensing objectives, autonomy level, communication conditions, human interaction, safety constraints, and success criteria. These parameters provide the basis for deriving engineering requirements and evaluating whether the platform is suitable.

The initial application scope should normally remain narrower than the theoretical capability of the robot. Attempting to support every terrain, payload, sensor, manipulation task, and autonomy mode from the beginning creates excessive integration complexity. A constrained operational design domain allows locomotion, perception, navigation, safety, and mission software to be validated against clearly defined conditions before the system expands toward more difficult environments.

Validation requirements should be derived directly from this operational design domain. If stair traversal is required, representative stairs must become part of testing. If the robot operates on gravel, slopes, or wet surfaces, those conditions must be included in mobility validation. If communication can disappear underground, communication-loss behavior must be tested. Application scope therefore becomes the foundation for meaningful software, hardware, and field-test criteria.

The target application scope ultimately defines what the quadruped must accomplish as a complete physical system. Locomotion provides access, perception provides environmental understanding, navigation determines movement, manipulation enables interaction, and mission software converts these capabilities into useful work. Safety, reliability, energy management, communication, and validation determine whether those capabilities can be deployed repeatedly outside controlled demonstrations.

A well-defined scope prevents quadruped development from becoming a collection of disconnected technologies. It connects morphology, actuators, sensing, state estimation, terrain perception, gait control, whole-body control, autonomy, manipulation, and Physical AI to measurable operational objectives. The correct question is therefore not simply how capable the quadruped can become, but which physical tasks it must perform reliably, safely, and repeatedly within a clearly defined environment.

4족 보행 로봇의 타깃 응용 분야(Target Application Scope)를 정의하는 것은 이동성 기술과 실제 운용 요구사항을 연결하는 시스템 엔지니어링 활동입니다. 4족 보행 로봇은 단지 다리 로코모션(Legged Locomotion)이 기술적으로 가능하다는 이유만으로 개발되어서는 안 됩니다. 그 진가는 기존 바퀴형 플랫폼의 유효성을 현저히 떨어뜨리는 계단, 장애물, 험로, 협소한 통로 또는 불연속적인 지면이 환경에 포함될 때 드러납니다.

응용 분야의 정의는 운용 환경에서 시작됩니다. 실내 공장, 발전소, 건설 현장, 지하 시설, 산림, 재난 지역, 야외 인프라는 저마다 서로 다른 이동성 요구사항을 부과합니다. 로코모션 능력과 감지(Sensing) 아키텍처를 선정하기 전에 표면 기하 구조, 경사도, 계단 치수, 바닥 강도, 가용 이격 거리, 조명, 날씨, 먼지, 수분, 온도, 통신 커버리지 등이 먼저 특성화되어야 합니다.

지형의 복잡성은 4족 보행 아키텍처를 선택하는 가장 강력한 이유 중 하나입니다. 평평하고 연속적인 지면은 기계적 단순성과 에너지 효율성 때문에 일반적으로 바퀴형 로봇에 유리합니다. 4족 보행 로봇은 단차, 돌더미, 간극, 불규칙한 지면, 식생, 가파른 경사, 또는 사람이 접근하도록 설계된 구조물을 건너야 할 때 비로소 강점을 가집니다. 따라서 해당 응용 분야는 다리 이동성이 수반하는 추가적인 기계적·계산적 복잡성을 정당화할 수 있어야 합니다.

산업용 점검(Industrial Inspection)은 많은 시설이 계단, 파이프, 플랫폼, 좁은 회랑, 그리고 다양한 고도에 분산된 설비들을 포함하고 있기 때문에 주요 타깃 응용 분야에 해당합니다. 4족 보행 로봇은 카메라, 열화상 카메라, 음향 센서, 가스 감지기, LiDAR 또는 기타 점검 계측기를 탑재한 채 지정된 경로를 따라 이동할 수 있습니다. 주된 목적은 단순히 걷는 것이 아니라, 유용한 측정 데이터를 수집해야 하는 위치로 감지 능력을 반복해서 이송하는 것입니다.

석유, 가스, 화학 및 에너지 시설은 대표적인 점검 환경을 제공합니다. 로봇은 계기판 관찰, 열 이상 감지, 누출 탐지, 설비 소음 기록, 구조 상태 점검, 공간 기록 생성 등을 수행하도록 요구받을 수 있습니다. 이러한 작업들은 이동 기술과 로컬라이제이션(Localization), 매핑, 미션 플래닝, 센서 포지셔닝, 데이터 로깅, 통신, 그리고 산업 인프라 주변에서의 안전한 운용의 통합을 필요로 합니다.

발전 및 유틸리티 환경 역시 유사한 요구사항을 생성하지만, 제한 구역, 전자기 간섭(EMI), 열, 수분, 밀폐 공간 또는 위험 설비와 같은 추가적인 위험 요소를 수반할 수 있습니다. 4족 보행 로봇은 반복적인 점검 경로를 수행함으로써 사람의 일상적인 위험 노출을 줄여줍니다. 그러나 실전 배치를 위해서는 예측 가능한 미션 완수, 신뢰성 높은 고장 처리, 그리고 감지, 로컬라이제이션, 통신 또는 전력이 저하되었을 때 안전한 위치로 복귀할 수 있는 능력이 필수적입니다.

건설 현장 모니터링은 환경이 지속적으로 변화하고 매끄러운 이동 Surface가 부족한 경우가 많아 또 다른 적합한 응용 분야입니다. 4족 보행 로봇은 가설 경사로, 미완성 바닥, 계단, 잔해, 불규칙한 지면을 통과하면서 영상이나 3차원 매핑 데이터를 수집할 수 있습니다. 반복적인 측량은 공정 모니터링, 치수 비교, 안전 점검, 그리고 공사진행에 따른 현장 상태의 문서화를 지원할 수 있습니다.

지하 광산, 터널, Subterranean 인프라는 거친 지형, 제한된 위성 항법, 먼지, 어둠, 통신 제약, 잠재적 위험 조건이 복합된 까다로운 환경입니다. 4족 보행 로봇은 바퀴형 로봇이 접지력을 유지하거나 장애물을 극복하기 어려운 곳에서 이동식 감지 기능을 제공할 수 있습니다. 이러한 응용 분야는 강건한 로컬 상태 추정, LiDAR 또는 비전 기반 로컬라이제이션, 지형 인지, 통신 회복력, 그리고 자율 복구 행동에 높은 요구사항을 부여합니다.

수색 구조(Search-and-Rescue) 및 재난 대응 환경은 더욱 가혹한 응용 클래스입니다. 붕괴된 구조물, 잔해, 불안정한 지면, 좁은 개구부, 열악한 시야, 불확실한 지도 등으로 인해 기존 이동 방식이 어려움을 겪을 수 있습니다. 4족 보행 로봇은 작업자에게 위험한 지역으로 카메라, 마이크, 환경 센서, 통신 중계기, 또는 경량 물자를 운송할 수 있으나, 지형 조건이 일반적인 로코모션 가정범위를 벗어날 수 있으므로 신뢰성과 운용자의 상황 파악 능력이 결정적인 요소가 됩니다.

산림, 농업, 자연 지형 응용 분야는 불규칙하고 변형 가능한 지면에 대한 적응을 강조합니다. 잔디, 뿌리, 자갈, 흙, 진흙, 경사면, 식생은 실험실 바닥과 현저히 다른 접촉 조건을 형성합니다. 성공적인 운용을 위해서는 시각적으로 깨끗한 모든 영역을 안전한 이동 가능 지역으로 취급하기보다, 강건한 접촉 추정, 슬립 처리, 지형 인식 기반의 발판(Foothold) 선택, 그리고 기하학적·기계적 위험 요소를 모두 식별할 수 있는 인지 능력이 요구됩니다.

보안 및 순찰 응용 분야는 계단이나 실내외 혼합 지형이 포함된 시설에서 4족 보행 로봇을 활용하여 정해진 경로를 반복 순찰할 수 있습니다. 로봇은 시각, 열화상, 음향, 환경 센서를 탑재하고 원격 운용자에게 이상 징후를 보고할 수 있습니다. 이 역할에서 이동성은 전체 시스템의 일부일 뿐입니다. 장시간 자율 운용, 충전, 플릿 관리(Fleet Management), 통신 보안, 이벤트 감지, 인간의 감독, 그리고 예측 가능한 안전 행동이 운용상의 유용성을 결정합니다.

원격 텔레프레전스(Telepresence)는 4족 보행 로봇이 원격 운용자의 이동형 아바타(Embodiment) 역할을 하는 또 다른 응용 카테고리입니다. 카메라, 마이크, 스피커, 환경 센서를 통해 운용자는 물리적으로 현장에 있지 않고도 위치를 점검하고 현장 인원과 상호작용할 수 있습니다. 다리 이동성은 텔레프레전스를 매끄러운 사무실 환경을 넘어 산업 공간, 야외 인프라, 계단이나 불규칙한 지면이 포함된 복잡한 시설로 확장해 줍니다.

페이로드 수송(Payload Transportation)은 자재, 공구, 센서, 물품을 기존 카트나 자율 이동 로봇(AMR)이 다니기 부적합한 지형을 통해 이동시켜야 할 때 고려될 수 있습니다. 해당 응용 분야에서는 페이로드 질량, 질량 중심(CoM) 변화, 요구 속도, 이동 거리, 지형의 가혹도, 로딩 방식을 명확히 정의해야 합니다. 적재 용량은 독립적으로 고려될 수 없는데, 추가 페이로드가 관절 토크, 접촉력, 에너지 소비, 안정성 여유도(Stability Margin), 열 부하에 직접적인 영향을 미치기 때문입니다.

로봇 암(Robotic Arm)이 장착된 4족 보행 로봇은 이동성을 로코-매니퓰레이션(Loco-manipulation)으로 확장합니다. 로봇은 설비를 단순히 관찰하는 것에 그치지 않고, 문을 열거나, 밸브를 돌리거나, 버튼을 누르거나, 손잡이를 조작하거나, 물체를 집어 올리거나, 센서를 목표 위치 근처에 정밀하게 배치할 수 있습니다. 이러한 작업들은 매니퓰레이션 반력과 균형, 로코모션을 결합하므로, 암과 이동 베이스를 독립된 로봇 시스템으로 다루기보다 협조된 전신 제어(Whole-body Control)를 필요로 합니다.

점검 매니퓰레이션은 센서를 정밀하게 위치시켜야 할 때 특히 유용합니다. 차체에 고정된 카메라는 설비 뒤에 숨겨진 계기판을 보지 못할 수 있지만, 다관절 암은 센서를 적절한 시야각으로 이동시킬 수 있습니다. 동일한 원리가 접촉식 프로브, 마이크, 열 센서, 또는 유지보수 공구에도 적용됩니다. 이 경우 4족 보행 로봇은 단순히 걷는 센서 운반체를 넘어 이동식 매니퓰레이션 플랫폼으로 기능합니다.

타깃 범위는 자율 운용(Autonomous Operation)과 원격 제어(Teleoperation)를 명확히 구분해야 합니다. 원격 제어는 자율성 요구사항을 낮춰줄 수 있지만 통신 품질과 운용자의 숙련도에 대한 의존도를 높입니다. 자율 미션은 로컬라이제이션, 지형 이해, 경로 계획, 장애물 회피, 로코모션 적응, 고장 감지 및 복구를 필요로 합니다. 많은 실용적인 시스템은 두 접근 방식을 결합하여, 일반적인 조건에서는 자율 실행을 허용하고 불확실성이 과도해질 때 인간이 개입할 수 있도록 합니다.

운용 반경(Operational Range)은 단순히 배터리 용량만으로 결정되지 않습니다. 에너지 소비는 지형, 보행 패턴(Gait), 페이로드, 속도, 온도, 그리고 반복적인 자세 전환에 따라 달라집니다. 미션 플래닝은 충전 구역이나 복구 위치로 돌아올 수 있는 충분한 에너지를 예비로 남겨두어야 합니다. 산업용 배치에서는 수동 작업 없이 반복적인 미션을 수행할 수 있도록 자동 도킹이나 배터리 관리 시스템이 추가로 요구될 수 있습니다.

응용 범위는 예상되는 로코모션 능력을 명시적으로 정의해야 합니다. 요구사항에는 보행 속도, 최소 통과 폭, 최대 경사도, 계단 치수, 장애물 높이, 지상 이격 거리(Ground Clearance), 회전 반경, 허용 발 슬립, 복구 능력 등이 포함될 수 있습니다. 이러한 요구사항은 단순히 \'우수한 야외 지형 이동성\'과 같은 모호한 목표에 의존하는 대신, 다리 워크스페이스, 액추에이터 토크, 차체 치수, 보행 패턴 선정, 인지 거리, 제어기 성능 등으로 번역되어야 합니다.

환경 보호 수준 역시 응용 분야에 따라 결정되어야 합니다. 실내 실험실 운용은 비교적 낮은 수준의 보호만 필요하지만, 필드 배치는 비, 먼지, 진흙, 진동, 온도 변화, 우발적 충격에 대한 저항성을 요구할 수 있습니다. 센서 윈도우, 관절, 커넥터, 배터리, 컴퓨터, 냉각 경로는 예상되는 조건 하에서도 정상적으로 작동해야 합니다. 따라서 환경적 강건성은 기계 설계, 전자 회로, 소프트웨어 모니터링, 유지보수 절차에 동시에 영향을 미칩니다.

통신 요구사항은 자율성의 수준과 운용 위험도에 따라 달라집니다. 원격 제어 로봇은 지속적인 저지연 통신을 필요로 하는 반면, 높은 수준의 자율 로봇은 일시적인 네트워크 단절 속에서도 미션을 계속 수행할 수 있습니다. 정지 요청과 같이 안전에 직결된 명령은 특히 신뢰성 있게 처리되어야 합니다. 시스템은 대역폭 감소, 패킷 손실, 완전한 통신 상실, 그리고 네트워크 연결 복구 시의 행동을 정의해야 합니다.

인간과의 상호작용은 4족 보행 로봇이 작업자나 일반 대중 주변에서 운용될 때 반드시 고려되어야 합니다. 운용자는 로봇의 상태, 미션 의도, 고장 유무, 안전 상태를 이해할 수 있어야 합니다. 속도 제한, 접근 금지 구역, 시청각 인디케이터, 비상 정지 메커니즘, 그리고 예측 가능한 정지 행동이 요구될 수 있습니다. 기술적으로 우수한 로코모션 시스템이라 할지라도 주변 인원이 그 행동을 예측하거나 안전하게 대응할 수 없다면 운용 측면에서 수용될 수 없습니다.

응용 범위는 적절한 수준의 인공지능(AI) 기술도 결정합니다. 학습 기반 로코모션은 지형 적응력을 향상시킬 수 있으며, 시맨틱 인지(Semantic Perception)는 의미 있는 객체와 영역을 식별할 수 있습니다. 비전-언어 모델(VLM)이나 파운데이션 모델 구성 요소는 미션 해석과 인간 상호작용을 지원할 수 있습니다. 이러한 기능들은 신뢰성 있는 물리적 운용을 위해 요구되는 확정적(Deterministic) 안전 메커니즘, 상태 추정, 운동 제약 조건, 그리고 하위 제어기를 대체하는 것이 아니라 보완해야 합니다.

다중 로봇 배치(Multi-robot Deployment)는 또 다른 응용 차원을 도입합니다. 여러 대의 4족 보행 로봇이 점검 구역을 분할하고, 지도를 공유하고, 통신을 중계하거나, 잉여 커버리지(Redundant Coverage)를 제공할 수 있습니다. 플릿 운용은 작업 할당, 미션 스케줄링, 지도 일관성, 충전 협조, 상태 모니터링, 복구 절차를 필요로 합니다. 따라서 추가 로봇 도입에 따른 이점은 개별 자율 로봇을 단순히 복제한다고 해서 자동으로 효과적인 협업이 이루어진다고 가정하기보다, 시스템 차원에서 평가되어야 합니다.

응용 분야 선택 시에는 4족 보행 이동성을 대체할 수 있는 대안들을 함께 고려해야 합니다. 바퀴형 자율 이동 로봇, 궤도형 차량, 드론, 고정형 센서, 또는 전통적인 인적 점검이 일부 작업들을 더 경제적으로 해결할 수 있습니다. 4족 보행 로봇은 인간 중심 환경이나 불규칙한 환경을 극복하는 능력이, 더 높은 비용, 에너지 소비, 유지보수 복잡성, 제어 요구사항을 상쇄할 만큼 충분한 운용 가치를 창출할 때 비로소 정당화됩니다.

따라서 실용적인 타깃 응용 분야는 단순히 점검이나 순찰과 같은 일반적인 진술이 아니라, 측정 가능한 운용 시나리오(Operational Scenario)로 표현되어야 합니다. 시나리오는 환경, 지형, 미션 시간, 페이로드, 감지 목표, 자율성 수준, 통신 조건, 인간 상호작용, 안전 제약 조건, 그리고 성공 기준을 명시해야 합니다. 이러한 파라미터들은 엔지니어링 요구사항을 도출하고 플랫폼의 적합성을 평가하는 기준을 제공합니다.

초기 응용 범위는 일반적으로 로봇의 이론적 한계 능력보다 좁게 유지되어야 합니다. 처음부터 모든 지형, 페이로드, 센서, 매니퓰레이션 작업, 자율성 모드를 지원하려 시도하는 것은 과도한 시스템 통합 복잡성을 초래합니다. 제약된 운용 설계 영역(ODD, Operational Design Domain)을 통해 로코모션, 인지, 항법, 안전, 미션 소프트웨어가 더 어려운 환경으로 확장되기 전, 명확히 정의된 조건에서 먼저 검증될 수 있습니다.

검증 요구사항은 이러한 운용 설계 영역으로부터 직접 도출되어야 합니다. 계단 이동이 요구된다면 대표적인 계단이 테스트의 일부가 되어야 합니다. 로봇이 자갈, 경사면, 습윤 표면에서 운용된다면 해당 조건들이 이동성 검증에 포함되어야 합니다. 지하에서 통신이 끊길 수 있다면 통신 상실 시의 행동이 테스트되어야 합니다. 따라서 응용 범위는 의미 있는 소프트웨어, 하드웨어 및 필드 테스트 기준의 기초가 됩니다.

타깃 응용 범위는 궁극적으로 4족 보행 로봇이 하나의 완결된 물리 시스템으로서 무엇을 달성해야 하는지를 정의합니다. 로코모션은 접근성을 제공하고, 인지는 환경 이해를 제공하며, 항법은 이동을 결정하고, 매니퓰레이션은 상호작용을 가능하게 하며, 미션 소프트웨어는 이러한 능력들을 유용한 작업으로 전환합니다. 안전성, 신뢰성, 에너지 관리, 통신, 그리고 검증은 이러한 능력들이 통제된 시연을 넘어 반복적으로 배치될 수 있는지 여부를 결정합니다.

잘 정의된 범위는 4족 보행 로봇 개발이 단절된 기술들의 집합체로 전락하는 것을 막아줍니다. 이는 형상(Morphology), 액추에이터, 감지, 상태 추정, 지형 인지, 보행 제어, 전신 제어, 자율성, 매니퓰레이션, 그리고 피지컬 AI(Physical AI)를 측정 가능한 운용 목표와 연결해 줍니다. 따라서 올바른 질문은 단순히 4족 보행 로봇이 얼마나 뛰어난 성능을 가질 수 있는가가 아니라, 명확히 정의된 환경 내에서 어떤 물리적 작업들을 신뢰성 있고 안전하며 반복적으로 수행해야 하는가입니다.
