**Volume 21. Quadruped Robot Software**

# Chapter 03. Gait Generation and Control

## 03.01. Gait Classification Walk Trot Canter Gallop Bound

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

보행 분류(Gait Classification)는 4족 로봇(Quadruped)이 이동하는 동안 네 개의 다리를 어떻게 협응(Coordinate)하는지를 체계적으로 설명하기 위한 프레임워크(Framework)를 제공한다. 보행(Gait)은 단순히 전진 속도만으로 정의되는 것이 아니라, 발 접촉(Foot Contact)의 시간적 순서, 입각기(Stance)와 유각기(Swing)의 지속 시간, 다리 사이의 위상 관계(Phase Relationship), 그리고 몸체를 지지하는 시간 구간에 의해 정의된다. 걷기(Walk), 트로트(Trot), 캔터(Canter), 갤럽(Gallop), 바운드(Bound)는 안정성(Stability), 속도(Speed), 에너지 효율(Energy Efficiency), 기동성(Maneuverability), 동적 성능(Dynamic Performance) 사이에서 서로 다른 절충 관계를 제공하는 대표적인 협응 패턴이다.

4족 보행(Quadruped Gait)을 표현하는 유용한 방법은 보행 주기(Gait Cycle)에서 시작한다. 보행 주기는 반복적인 이동 과정에서 다리의 구성이 동일한 위상 상태로 되돌아오는 하나의 시간 구간으로 정의된다. 각각의 다리는 발이 지면과 상호작용하며 지지력을 발생시키는 입각기(Stance)와 발이 다음 접촉 위치를 향해 이동하는 유각기(Swing)를 교대로 반복한다. 전체 보행 주기에 대한 입각기 지속 시간의 비율을 듀티 팩터(Duty Factor)라고 하며, 이는 정적 보행(Static Gait)과 동적 보행(Dynamic Gait)을 구분하는 중요한 변수이다.

걷기(Walk)는 일반적으로 비교적 높은 듀티 팩터(Duty Factor)와 여러 다리 사이에서 중첩되는 지면 접촉 구간을 특징으로 한다. 일반적인 4족 걷기에서는 대각선 또는 좌우 다리 쌍이 동시에 움직이기보다 각각의 발이 순차적으로 지면에 접촉한다. 보행 주기의 상당 부분에서 최소 두 개 또는 세 개의 발이 지면과 접촉한다. 이러한 특성은 비교적 넓은 지지 영역(Support Region)을 형성하며 저속 이동에서 무게중심(Center of Mass)을 안정적으로 제어할 수 있도록 한다.

걷기(Walk)는 지면 지지를 충분히 유지하기 때문에 속도보다 안정성과 지형 적응성(Terrain Adaptability)이 중요한 상황에서 특히 유용하다. 4족 로봇은 거친 지면, 좁은 통로, 경사면, 계단 또는 불확실한 지형에서 걷기를 자주 사용한다. 각 발의 착지 위치(Foothold)를 비교적 작은 동적 교란(Dynamic Disturbance)으로 선택하고 수정할 수 있기 때문이다. 제어기(Controller)는 지지 상태에 있는 나머지 다리를 통해 지지력을 재분배하면서 각각의 유각 궤적(Swing Trajectory)을 독립적으로 조절할 수 있다.

트로트(Trot)는 대각선 방향의 두 다리가 거의 동시에 움직이는 비교적 빠른 대칭 보행(Symmetric Gait)이다. 왼쪽 앞다리(Front-Left)와 오른쪽 뒷다리(Rear-Right)가 하나의 다리 쌍을 형성하고, 오른쪽 앞다리(Front-Right)와 왼쪽 뒷다리(Rear-Left)가 다른 다리 쌍을 형성한다. 두 대각선 다리 쌍은 약 반 주기(Half-Cycle)의 위상 차이를 가지며 입각기와 유각기를 교대로 수행한다. 이러한 대칭성은 이동 속도, 기계적 단순성, 동적 안정성(Dynamic Stability), 그리고 제어 계산의 복잡성 사이에서 효과적인 균형을 제공한다.

트로트(Trot)에서는 일반적으로 하나의 대각선 다리 쌍이 몸체를 지지한 후 반대쪽 대각선 다리 쌍으로 지지가 전환된다. 속도가 증가하면 접촉 사이에 짧은 공중 구간(Aerial Phase)이 발생할 수 있으며, 이에 따라 움직임은 더욱 동적인 러닝 트로트(Running Trot)로 변화한다. 따라서 지면 반력(Ground Reaction Force), 몸체 관성(Body Inertia), 운동량(Momentum)의 중요성이 증가한다. 모델 예측 제어(Model Predictive Control), 중심 동역학(Centroidal Dynamics), 전신 제어(Whole-Body Control)는 원하는 몸체 자세와 속도를 유지하면서 이러한 힘을 협응시키는 데 일반적으로 사용된다.

캔터(Canter)는 개념적으로 트로트(Trot)와 갤럽(Gallop) 사이에 위치하는 비대칭 보행(Asymmetric Gait)이다. 트로트의 대각선 대칭성과 달리 캔터는 선행 다리(Leading Leg)가 존재하는 순차적인 다리 접촉 패턴을 사용한다. 동물 또는 로봇의 구현 방식에 따라 세 박자(Three-Beat) 또는 이와 유사한 비대칭 리듬이 형성된다. 이 보행은 왼쪽과 오른쪽 선행 다리를 구분하기 때문에 선행 다리를 변경하면 빠른 기동 과정에서 회전 동작, 몸체 자세, 기계적 하중 분포에 영향을 줄 수 있다.

4족 로봇에서 캔터(Canter)는 걷기(Walk)나 트로트(Trot)보다 기본 이동 방식으로 사용되는 경우가 적지만, 보행 전환(Transition)과 비대칭 이동을 연구하는 데 중요한 의미가 있다. 로봇의 캔터를 구현하려면 위상 오프셋(Phase Offset), 접촉 타이밍(Contact Timing), 몸체 피치(Body Pitch), 운동량 전달(Momentum Transfer)을 정밀하게 제어해야 한다. 캔터는 고속 이동으로 가속하는 과정을 부드럽게 만들 수 있으며, 완전히 대칭적인 발 접촉 패턴이 로봇의 동적 움직임을 불필요하게 제한하는 상황에서 방향 전환 기동을 지원할 수 있다.

갤럽(Gallop)은 앞다리와 뒷다리가 특징적인 순서로 지면에 접촉하며 몸체 운동량이 크게 변화하는 고속 비대칭 보행(High-Speed Asymmetric Gait)이다. 위상 패턴에 따라 갤럽은 횡 갤럽(Transverse Gallop) 또는 회전 갤럽(Rotary Gallop) 형태로 분류할 수 있다. 걷기나 중간 속도의 트로트와 달리 갤럽은 공중 구간(Aerial Phase), 탄성 에너지 교환(Elastic Energy Exchange), 몸체 피칭 운동(Body Pitching Motion), 빠른 지면 반력 생성과 같은 동적 효과(Dynamic Effect)에 크게 의존한다.

갤럽(Gallop) 과정에서는 안정성이 준정적 균형(Quasi-Static Balance)보다 동적 운동량(Dynamic Momentum)에 의해 주로 결정되기 때문에 무게중심(Center of Mass)이 전통적인 정적 지지 다각형(Static Support Polygon)의 외부로 이동할 수 있다. 따라서 성공적인 제어를 위해서는 미래의 접촉 상태와 몸체 움직임을 정확하게 예측해야 한다. 발 배치(Foot Placement), 착지 속도(Touchdown Velocity), 접촉 충격량(Contact Impulse), 액추에이터 한계(Actuator Limit), 마찰 제약조건(Friction Constraint)이 핵심 변수가 된다. 고속에서는 로봇이 상당한 운동에너지를 가지므로 작은 타이밍 오차도 큰 교란을 발생시킬 수 있다.

바운드(Bound)는 두 앞다리가 거의 동시에 움직이고 두 뒷다리 역시 거의 동시에 움직이는 또 다른 고동적 보행(Highly Dynamic Gait)이다. 앞다리 쌍과 뒷다리 쌍은 교대로 움직이며, 두 접촉 사이에 공중 구간(Aerial Phase)이 발생하는 경우가 많다. 이 과정에서는 스프링이 장착된 몸체가 압축과 신장을 반복하는 것과 유사한 뚜렷한 피칭 운동(Pitching Motion)이 나타난다. 바운드는 빠른 전진 이동에 특히 적합하며 고동적 4족 제어(Highly Dynamic Quadruped Control)를 연구하기 위한 유용한 실험적 보행을 제공한다.

바운드(Bound)의 효율성은 로봇의 앞부분과 뒷부분 사이에서 이루어지는 협응된 에너지 전달(Coordinated Energy Transfer)에 크게 의존한다. 뒷다리는 강력한 추진력(Propulsion)을 생성할 수 있으며 앞다리는 착지 과정에서 충격을 흡수하고 운동량의 방향을 변경한다. 반복적인 접촉으로 불안정한 회전 운동이 발생하지 않도록 몸체 피치(Body Pitch)를 세밀하게 제어해야 한다. 순응성 다리(Compliant Leg), 탄성 요소(Elastic Element), 능동적으로 제어되는 관절 임피던스(Joint Impedance)를 가진 로봇은 저장된 기계적 에너지를 활용하여 바운드 효율을 향상시킬 수 있다.

이러한 보행 사이의 차이는 상대적인 다리 위상(Relative Limb Phase)을 통해 수학적으로 표현할 수 있다. 보행 주기 동안 각각의 다리에 0에서 1 사이의 위상 변수(Phase Variable)를 할당하면 네 다리 사이의 위상 오프셋(Phase Offset)을 이용하여 보행 패턴을 표현할 수 있다. 걷기(Walk)는 각 다리의 위상을 주기 전체에 분산시키고, 트로트(Trot)는 대각선 다리를 하나의 그룹으로 묶으며, 바운드(Bound)는 앞다리와 뒷다리를 각각 그룹화한다. 반면 캔터(Canter)와 갤럽(Gallop)은 비대칭적인 위상 오프셋을 사용한다. 이러한 표현을 사용하면 하나의 공통 수학적 프레임워크를 이용하여 여러 종류의 보행을 생성할 수 있다.

접촉 스케줄(Contact Schedule)은 로봇 제어에서 사용할 수 있는 또 다른 실용적인 표현 방법이다. 보행을 생물학적인 명칭으로만 설명하는 대신 이동 시스템은 예측 구간(Prediction Horizon) 동안 각각의 발이 언제 입각기 또는 유각기에 있어야 하는지를 정의한다. 보행 생성기(Gait Generator)는 목표 속도, 지형 정보, 안정성 요구조건을 접촉 순서로 변환할 수 있다. 이러한 스케줄은 궤적 최적화(Trajectory Optimization), 모델 예측 제어(Model Predictive Control), 발걸음 계획(Footstep Planning), 강화학습 기반 이동 정책(Reinforcement-Learning-Based Locomotion Policy)의 기준 입력(Reference Input)으로 사용된다.

보행 전환(Gait Transition)은 각각의 개별 보행 패턴만큼 중요하다. 4족 로봇은 안정적인 걷기(Walk)로 이동을 시작한 후 명령 속도가 증가하면 트로트(Trot)로 전환하고, 더 높은 동적 성능이 필요한 경우 캔터(Canter), 갤럽(Gallop), 바운드(Bound)로 이동할 수 있다. 하나의 접촉 순서를 다른 접촉 순서로 갑작스럽게 변경하면 로봇이 불안정해질 수 있다. 따라서 실제 보행 전환 알고리즘은 실현 가능한 접촉력을 유지하면서 듀티 팩터(Duty Factor), 위상 오프셋(Phase Offset), 보폭 주파수(Stride Frequency), 보폭 길이(Step Length)를 점진적으로 변경한다.

보행 선택(Gait Selection)은 속도만으로 결정해서는 안 된다. 지형 형상(Terrain Geometry), 마찰(Friction), 탑재 하중(Payload), 액추에이터 온도(Actuator Temperature), 배터리 상태(Battery Condition), 외부 교란(External Disturbance), 임무 목표(Mission Objective)에 따라 가장 적합한 보행이 달라질 수 있다. 무거운 하중을 탑재한 4족 로봇은 높은 속도 명령을 받더라도 걷기를 선택할 수 있으며, 예측 가능한 지형에서 하중이 없는 로봇은 트로트나 바운드를 안전하게 사용할 수 있다. 따라서 지능형 이동 시스템(Intelligent Locomotion System)은 보행 선택을 단순한 속도 기반 참조표가 아니라 제약조건을 가진 의사결정 문제(Constrained Decision Problem)로 다룬다.

지형 인식(Terrain Perception)은 보행 분류의 역할을 더욱 확장한다. 평탄한 지면에서는 주기적인 접촉 타이밍만으로 충분할 수 있지만 불규칙한 지형에서는 착지 위치 적응(Foothold Adaptation)이 필요하며 경우에 따라 명목 보행(Nominal Gait)에서 일시적으로 벗어나야 한다. 안전한 착지 위치를 확보할 수 없는 경우 로봇은 하나의 입각기를 단축하고 다른 입각기를 연장하거나 유각 다리의 움직임을 지연할 수 있다. 따라서 실제 이동 제어는 명목 보행 템플릿(Nominal Gait Template)과 환경 조건에 따라 접촉 타이밍과 발 궤적을 지속적으로 수정하는 피드백 메커니즘(Feedback Mechanism)을 결합한다.

보행 생성(Gait Generation)은 로봇의 기계적 설계(Mechanical Design)와 밀접하게 연결되어 있다. 다리 길이(Leg Length), 관절 운동 범위(Joint Range), 액추에이터 토크(Actuator Torque), 반사 관성(Reflected Inertia), 발 형상(Foot Geometry), 순응성(Compliance), 몸체 질량 분포(Body Mass Distribution)는 어떤 보행 패턴을 효과적으로 수행할 수 있는지를 결정한다. 제어기는 물리적으로 실현할 수 없는 접촉력이나 관절 속도를 만들어낼 수 없다. 따라서 보행 분류는 생물학적 보행 용어를 독립적인 소프트웨어 추상화로 취급하기보다 로봇이 실제로 구현할 수 있는 동적 운용 범위(Dynamic Envelope)와 함께 해석해야 한다.

현대의 학습 기반 이동(Learning-Based Locomotion)은 전통적인 보행 사이의 경계를 모호하게 만들 수 있다. 강화학습 정책(Reinforcement-Learning Policy)은 걷기, 트로트, 캔터, 갤럽, 바운드 가운데 어느 하나와 정확히 일치하지 않는 중간 또는 하이브리드 패턴(Hybrid Pattern)을 발견할 수 있다. 그럼에도 전통적인 보행 분류는 초기화(Initialization), 커리큘럼 학습(Curriculum Learning), 정책 평가(Policy Evaluation), 안전 제약조건(Safety Constraint)을 위한 해석 가능한 구조를 제공한다는 점에서 여전히 중요하다. 또한 학습된 정책을 보행 매개변수에 조건화하여 서로 다른 이동 행동 사이를 연속적으로 보간(Interpolation)하도록 구성할 수 있다.

피지컬 AI(Physical AI)의 관점에서 보행(Gait)은 인식(Perception), 동역학(Dynamics), 제어(Control), 환경 상호작용(Environmental Interaction)을 연결하는 체화된 협응 전략(Embodied Coordination Strategy)이다. 로봇은 지형과 내부 상태를 인식하고, 실현 가능한 접촉을 예측하며, 협응된 다리 움직임을 생성하고, 접촉력을 조절하며, 기존 가정이 더 이상 유효하지 않을 때 행동을 적응시켜야 한다. 따라서 보행 분류는 단순한 용어 체계를 넘어 물리적 지능(Physical Intelligence)이 환경과의 복잡한 전신 상호작용(Whole-Body Interaction)을 조직하는 재사용 가능한 패턴을 정의한다.

궁극적으로 걷기(Walk), 트로트(Trot), 캔터(Canter), 갤럽(Gallop), 바운드(Bound)는 위상(Phase), 듀티 팩터(Duty Factor), 보폭 주파수(Stride Frequency), 접촉 순서(Contact Sequence), 몸체 동역학(Body Dynamics), 힘 분포(Force Distribution)에 의해 매개변수화되는 더 넓은 이동 공간(Locomotion Space)의 서로 다른 영역으로 이해할 수 있다. 유능한 4족 로봇 제어기는 이러한 패턴을 단순히 재현하는 데 그치지 않고 임무 요구조건에 따라 적절한 보행을 선택하고, 보행 사이를 전환하며, 환경 변화에 맞추어 적응시킬 수 있어야 한다. 이러한 관점에서 보행 생성은 고정된 애니메이션 문제가 아니라 안정적이고 효율적이며 지능적인 물리적 행동을 지속적으로 최적화하는 문제로 확장된다.

## 03.02. Gait Pattern Parameterization Phase Offset Duty [w/Code]

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

보행 패턴 매개변수화(Gait Pattern Parameterization)는 4족 로봇 이동(Quadruped Locomotion)에서 협응된 다리 움직임을 설명하고 생성하기 위한 간결한 수학적 방법을 제공한다. 각각의 관절 궤적(Joint Trajectory)을 독립적으로 정의하는 대신, 제어기(Controller)는 보행 위상(Gait Phase), 다리 위상 오프셋(Limb Phase Offset), 듀티 팩터(Duty Factor), 주기 주파수(Cycle Frequency), 입각 지속 시간(Stance Duration), 유각 지속 시간(Swing Duration)과 같은 소수의 변수를 이용하여 이동을 표현한다. 이러한 매개변수는 이동의 시간적 구조를 하위 수준 관절 제어(Lower-Level Joint Control)와 분리할 수 있도록 한다.

많은 보행 생성기(Gait Generator)에서 중심이 되는 변수는 보행 위상(Gait Phase)이다. 정규화된 위상 변수(Normalized Phase Variable)는 일반적으로 하나의 이동 주기 동안 0에서 1까지 증가한 후 다시 0으로 되돌아간다. 또는 위상을 0에서 2π까지의 각도로 표현할 수도 있다. 위상은 로봇이 현재 보행 주기에서 어느 위치에 있는지를 나타내는 공통 내부 시계(Common Internal Clock)를 제공하며, 주기적인 다리 움직임을 일관된 수학적 기준에 따라 동기화할 수 있도록 한다.

각각의 다리에는 전역 보행 위상(Global Gait Phase)으로부터 유도된 개별 위상(Individual Phase)을 할당할 수 있다. 다리 i의 위상은 개념적으로 전역 위상에 해당 다리의 고유한 위상 오프셋(Phase Offset)을 더하고, 그 결과를 하나의 주기 범위 안으로 순환시키는 방식으로 표현할 수 있다. 위상 오프셋은 해당 다리와 다른 다리 사이의 시간적 관계를 결정한다. 이러한 오프셋만 변경함으로써 공통 보행 생성기는 전체 제어기를 다시 설계하지 않고도 상당히 다른 협응 패턴(Coordination Pattern)을 구현할 수 있다.

위상 오프셋(Phase Offset)은 보행 대칭성(Gait Symmetry)을 표현하는 데 특히 유용하다. 트로트(Trot)에서는 일반적으로 대각선 다리들이 유사한 위상을 공유하며, 두 대각선 다리 쌍은 약 반 주기(Half Cycle)의 차이를 갖는다. 바운드(Bound)에서는 두 앞다리가 하나의 동기화 그룹을 형성하고 두 뒷다리가 또 다른 그룹을 형성한다. 걷기(Walk)는 네 다리의 위상을 보행 주기 전체에 보다 균등하게 분산시킨다. 캔터(Canter)와 갤럽(Gallop) 같은 비대칭 패턴은 특정 접촉 순서를 형성하기 위해 서로 다른 크기의 위상 오프셋을 필요로 한다.

듀티 팩터(Duty Factor)는 하나의 보행 주기 중 발이 지면과 입각 접촉(Stance Contact)을 유지하는 시간의 비율을 나타낸다. 예를 들어 듀티 팩터가 0.6이라면 해당 발은 전체 주기의 약 60퍼센트를 입각 상태로 보내고 나머지 40퍼센트를 유각 상태로 보낸다. 이처럼 단순해 보이는 매개변수는 지지 형상(Support Geometry), 힘 생성 가능 시간, 동적 거동(Dynamic Behavior), 에너지 소비(Energy Consumption), 그리고 이동 과정에서 운동량(Momentum)에 의존하는 정도에 큰 영향을 미친다.

높은 듀티 팩터(Duty Factor)는 일반적으로 더 긴 입각 구간과 지지 발 사이의 더 큰 접촉 중첩(Contact Overlap)을 만든다. 이러한 패턴은 로봇이 지면 반력(Ground Reaction Force)을 생성하고 무게를 재분배할 수 있는 시간이 길기 때문에 느리고 안정적인 이동에 적합하다. 듀티 팩터가 감소하면 입각 구간은 짧아지고 유각 구간이 전체 주기에서 차지하는 비율은 증가한다. 이에 따라 동적 효과(Dynamic Effect)가 점점 중요해지며, 어떤 발도 지면과 접촉하지 않는 공중 구간(Aerial Phase)이 발생할 수 있다.

위상 오프셋(Phase Offset)과 듀티 팩터(Duty Factor)의 조합은 주기적 보행(Periodic Gait)의 접촉 구조(Contact Structure) 대부분을 결정한다. 위상 오프셋은 각각의 다리가 주기의 특정 구간에 언제 진입하는지를 결정하고, 듀티 팩터는 해당 다리가 입각 상태에 얼마나 오래 머무르는지를 결정한다. 따라서 동일한 위상 오프셋을 가진 두 보행도 듀티 팩터가 다르면 상당히 다른 동적 특성을 나타낼 수 있다. 이러한 분리를 통해 비교적 저차원의 매개변수 공간(Parameter Space)에서 이동 패턴을 체계적으로 탐색할 수 있다.

주기 주파수(Cycle Frequency)는 또 다른 핵심 보행 매개변수이다. 이는 단위 시간당 몇 번의 완전한 보행 주기가 수행되는지를 나타내며, 따라서 발걸음 타이밍(Step Timing)과 이동 속도에 직접적인 영향을 미친다. 주기 시간(Cycle Period)은 주파수의 역수이다. 듀티 팩터를 동시에 변경하지 않은 상태에서 주파수를 증가시키면 입각 시간과 유각 시간이 모두 짧아진다. 제어기는 요구되는 관절 속도, 가속도, 접촉력이 로봇의 물리적 성능 범위 안에 있도록 보장해야 한다.

보폭 길이(Stride Length)는 보행 주파수(Gait Frequency)와 상호작용하여 전진 속도를 결정한다. 로봇은 보폭을 길게 하거나, 주기 주파수를 증가시키거나, 두 가지 방법을 함께 사용하여 속도를 높일 수 있다. 그러나 각각의 방법은 서로 다른 기계적 요구조건을 발생시킨다. 지나치게 긴 보폭은 관절 작업 공간(Joint Workspace)의 한계에 접근할 수 있으며, 지나치게 높은 주파수는 높은 액추에이터 속도를 요구하고 큰 관성력(Inertial Force)을 발생시킬 수 있다. 따라서 실제 보행 매개변수화에서는 로봇의 형태(Morphology)와 액추에이터 성능에 따라 주파수와 보폭 길이를 제한한다.

입각 지속 시간(Stance Duration)과 유각 지속 시간(Swing Duration)은 보행 주기와 듀티 팩터로부터 직접 계산할 수 있다. T가 전체 보행 주기이고 D가 듀티 팩터라면 입각 지속 시간은 대략 D와 T의 곱으로 표현되며, 유각 지속 시간은 대략 1-D와 T의 곱으로 표현된다. 이러한 시간은 입각 제어가 주로 힘 생성과 몸체 안정화를 담당하는 반면, 유각 제어는 발의 지면 여유 높이(Foot Clearance), 궤적 형상(Trajectory Shaping), 다음 착지 준비를 담당하기 때문에 중요하다.

각 다리의 주기 내부에서 정규화된 위상(Normalized Phase)은 입각 하위 위상(Stance Subphase)과 유각 하위 위상(Swing Subphase)으로 나눌 수 있다. 위상이 듀티 팩터에 의해 결정되는 입각 구간 안에 있을 때 제어기는 해당 발을 계획된 접촉(Planned Contact)으로 처리하고 적절한 지면 반력을 생성한다. 위상이 입각-유각 경계(Stance-to-Swing Boundary)를 통과하면 해당 발은 지지 상태에서 해제되어 유각 궤적을 따라 이동한다. 이러한 위상 기반 상태 기계(Phase-Based State Machine)는 보행 타이밍과 전신 제어(Whole-Body Control)를 연결하는 간단한 인터페이스를 제공한다.

유각 위상 매개변수화(Swing Phase Parameterization)는 일반적으로 이륙(Liftoff) 시점의 0에서 착지(Touchdown) 시점의 1까지 진행되는 추가적인 정규화 변수를 사용한다. 이 국부 유각 위상(Local Swing Phase)은 다항식(Polynomial), 베지어 곡선(Bézier), 스플라인(Spline), 또는 학습 기반 발 궤적(Learned Foot Trajectory)을 생성하는 데 사용할 수 있다. 이후 발걸음 높이(Step Height), 착지 위치(Touchdown Position), 여유 높이 마진(Clearance Margin), 착지 속도(Touchdown Velocity)와 같은 매개변수를 전역 보행 타이밍과 독립적으로 변경할 수 있다. 이러한 모듈식 구조(Modular Structure)는 명목 보행 패턴을 근본적으로 변경하지 않고도 지형에 적응할 수 있도록 한다.

입각 위상(Stance Phase) 역시 착지부터 이륙까지 국부적으로 매개변수화할 수 있다. 입각 중에는 몸체가 발 위로 이동하는 동안 목표 발 위치(Desired Foot Position)가 지면에 대해 거의 고정되도록 설정할 수 있으며, 또는 순응성(Compliance)과 지형 상호작용(Terrain Interaction)에 따라 조정할 수도 있다. 힘 제어기(Force Controller)는 계획된 접촉 상태와 목표 몸체 가속도를 이용하여 마찰, 토크, 접촉 제약조건을 만족시키면서 지지 다리 사이에 지면 반력을 분배한다.

접촉 테이블(Contact Table)은 연속적인 보행 매개변수로부터 생성되는 이산 표현(Discrete Representation)을 제공한다. 각각의 예측 단계(Prediction Step)에서 모든 다리는 위상 오프셋과 듀티 팩터에 따라 입각 또는 유각 상태로 지정된다. 모델 예측 제어(Model Predictive Control)는 이러한 미래 접촉 스케줄(Future Contact Schedule)을 이용하여 각 시점에서 사용할 수 있는 지면 반력을 결정할 수 있다. 따라서 간결한 위상 매개변수를 최적화 기반 이동 제어기(Optimization-Based Locomotion Controller)에 필요한 명시적인 접촉 제약조건(Contact Constraint)으로 변환할 수 있다.

부드러운 보행 전환(Smooth Gait Transition)을 위해서는 갑작스러운 전환보다 매개변수 보간(Parameter Interpolation)이 필요하다. 로봇이 걷기에서 트로트로 전환한다면 실현 가능한 접촉 상태를 유지하면서 위상 오프셋, 듀티 팩터, 주파수, 그리고 필요에 따라 보폭 길이를 점진적으로 변화시켜야 한다. 하나의 위상 구성을 다른 구성으로 직접 교체하면 조기 이륙(Premature Liftoff)이나 예상하지 못한 착지(Unexpected Touchdown)가 발생할 수 있다. 따라서 전환 관리자(Transition Manager)는 발 접촉, 위상 경계 또는 동역학적으로 유리한 지지 구성과 같은 적절한 이벤트에 맞추어 매개변수 변화를 동기화한다.

실제 접촉 이벤트가 명목 스케줄(Nominal Schedule)과 다를 경우 위상 동기화(Phase Synchronization) 역시 중요하다. 지면이 예상보다 높으면 발이 계획보다 일찍 접촉할 수 있고, 지면이 낮으면 접촉이 지연될 수 있다. 이때 개루프 위상 시계(Open-Loop Phase Clock)를 엄격하게 따르게 되면 실제 접촉 상태와 제어기의 접촉 가정 사이에 불일치가 발생할 수 있다. 이벤트 기반 위상 보정(Event-Based Phase Correction)은 측정된 착지 및 이륙 이벤트를 이용하여 선택된 위상 변수를 앞당기거나 지연시키거나 재설정함으로써 불규칙한 지면에서의 강건성(Robustness)을 향상시킨다.

적응형 보행 매개변수화(Adaptive Gait Parameterization)는 로봇 상태와 환경 조건에 따라 매개변수가 변경될 수 있도록 이러한 개념을 확장한다. 목표 속도는 주기 주파수와 보폭 길이를 변경할 수 있으며, 지형 거칠기(Terrain Roughness)가 증가하면 듀티 팩터와 발 여유 높이를 증가시킬 수 있다. 탑재 하중(Payload)이 증가하면 더 긴 입각 시간이 유리할 수 있고, 낮은 마찰에서는 가속도를 줄이고 접촉 중첩을 증가시켜야 할 수 있다. 따라서 보행 매개변수는 사전에 정의된 보행 라이브러리에 저장된 고정 상수가 아니라 제어 변수(Control Variable)가 된다.

연속 매개변수화(Continuous Parameterization)를 사용하면 이름이 부여된 기존 보행 사이의 중간 패턴도 생성할 수 있다. 제어기는 걷기, 트로트, 바운드와 같은 이산적인 모드만 전환하는 대신 실현 가능한 범위 안에서 위상 관계와 듀티 팩터를 연속적으로 변경할 수 있다. 이를 통해 속도나 지형 변화에 따라 이동 행동을 점진적으로 변화시킬 수 있다. 그러나 모든 수학적 조합이 물리적으로 유용한 보행을 만드는 것은 아니므로 안정성, 충돌, 힘, 운동학, 액추에이터 제약조건을 이용하여 허용 가능한 매개변수 영역을 제한해야 한다.

최적화 기반 방법(Optimization-Based Method)은 성능 목표에 따라 이러한 매개변수 공간을 탐색할 수 있다. 에너지 소비(Energy Consumption), 추종 오차(Tracking Error), 안정성 여유(Stability Margin), 충격력(Impact Force), 지형 여유 높이(Terrain Clearance), 액추에이터 작동량(Actuator Effort) 등을 목적 함수(Objective Function)에 포함할 수 있다. 최적화기는 현재 임무를 가장 잘 만족시키는 주파수, 듀티 팩터, 위상 오프셋, 착지 타이밍, 보폭 매개변수를 선택할 수 있다. 이러한 매개변수화는 각각의 관절 궤적을 직접 최적화하는 방식과 비교하여 탐색 공간의 차원을 줄여준다.

학습 기반 이동(Learning-Based Locomotion)에서도 동일한 매개변수를 명령(Command), 관측값(Observation), 또는 잠재 변수(Latent Variable)로 사용할 수 있다. 강화학습 정책(Reinforcement-Learning Policy)은 목표 보행 주파수, 위상 오프셋, 듀티 팩터를 입력받고 명령된 접촉 패턴을 구현하는 관절 동작을 학습할 수 있다. 또는 상위 수준 정책(High-Level Policy)이 보행 매개변수를 선택하고 하위 수준 제어기(Low-Level Controller)가 이를 실행하도록 구성할 수 있다. 이러한 계층적 구조(Hierarchical Organization)는 해석 가능한 보행 구조와 학습된 전신 행동의 적응성을 결합한다.

위상 변수(Phase Variable)는 사인(Sine)과 코사인(Cosine) 표현을 통해 신경망 관측값(Neural-Network Observation)에 직접 포함할 수도 있다. 위상을 sin(2πφ)와 cos(2πφ)로 인코딩하면 정규화된 위상이 1에서 다시 0으로 순환할 때 발생하는 수치적 불연속성(Numerical Discontinuity)을 방지할 수 있다. 정책은 이동 타이밍에 대한 부드러운 주기 표현(Smooth Periodic Representation)을 입력받고 특정 위상을 적절한 관절 구성, 접촉력, 또는 예측 행동(Anticipatory Action)과 연관시킬 수 있다.

피지컬 AI(Physical AI) 시스템에서 보행 매개변수화(Gait Parameterization)는 상위 수준 의도(High-Level Intent)와 체화된 동역학(Embodied Dynamics)을 연결하는 인터페이스 역할을 한다. 더 빠르게 이동하거나, 신중하게 경사면을 오르거나, 무거운 하중을 운반하거나, 미끄러운 지형을 통과하라는 명령은 주파수, 듀티 팩터, 위상 관계, 보폭 형상(Stride Geometry), 접촉 타이밍의 변화로 변환될 수 있다. 이후 하위 수준 제어는 이러한 추상적인 시간 매개변수를 물리적으로 실현 가능한 관절 토크와 지면 상호작용으로 변환한다.

따라서 강건한 보행 생성기(Robust Gait Generator)는 위상 오프셋과 듀티 팩터를 서로 독립된 수치 설정으로 취급해서는 안 된다. 이들은 주파수, 입각 및 유각 타이밍, 발걸음 형상(Step Geometry), 접촉 제약조건, 지형 정보, 로봇 동역학을 포함하는 통합 매개변수 공간(Integrated Parameter Space)의 일부를 구성한다. 이러한 간결한 표현을 중심으로 이동을 구성하면 4족 로봇은 여러 보행을 생성하고, 보행 사이를 부드럽게 전환하며, 접촉 스케줄을 온라인으로 적응시키고, 계획(Planning), 학습(Learning), 전신 제어 사이에서 일관된 인터페이스를 유지할 수 있다.

## 03.03. Contact Schedule Generation and Adaptation [w/Code]

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

접촉 스케줄 생성(Contact Schedule Generation)은 4족 로봇의 각 발이 언제 환경과 접촉을 시작하고, 유지하며, 해제해야 하는지를 정의한다. 이는 추상적인 보행 설명(Gait Description)을 이동 제어기에서 직접 사용할 수 있는 시간 종속적인 입각(Stance) 및 유각(Swing) 상태의 순서로 변환한다. 접촉은 로봇에 힘이 전달되는 방식을 결정하므로 접촉 스케줄은 보행 생성(Gait Generation), 궤적 계획(Trajectory Planning), 동역학 최적화(Dynamics Optimization), 전신 제어(Whole-Body Control)를 연결하는 핵심 인터페이스를 형성한다.

접촉 스케줄(Contact Schedule)은 시간에 따라 각 다리에 대한 이진 상태(Binary State)로 표현할 수 있다. 입각에 해당하는 값은 발이 몸체를 지지하고 지면 반력(Ground Reaction Force)을 생성할 것으로 예상된다는 것을 의미하며, 유각 상태는 발이 새로운 착지 위치(Foothold)를 향해 이동하고 있음을 의미한다. 네 다리의 상태를 결합하면 4족 로봇의 순간적인 지지 구성(Instantaneous Support Configuration)을 나타내는 접촉 모드(Contact Mode)가 형성되며, 이를 통해 어떤 동적 제약조건(Dynamic Constraint)이 적용되는지가 결정된다.

주기적 보행 매개변수(Periodic Gait Parameter)는 명목 접촉 스케줄(Nominal Contact Schedule)을 구성하는 간단한 방법을 제공한다. 전역 보행 위상(Global Gait Phase)은 명령된 주기 주파수(Cycle Frequency)에 따라 진행되며, 개별 위상 오프셋(Phase Offset)은 각 다리의 상대적인 타이밍을 결정한다. 듀티 팩터(Duty Factor)는 각 주기에서 입각에 할당되는 시간의 비율을 지정한다. 각 제어 시점에서 이러한 변수를 평가하면 독립적인 타이밍 순서를 별도로 설계하지 않고도 각 다리에 대한 계획된 입각 및 유각 상태를 생성할 수 있다.

서로 다른 보행 유형(Gait Family)은 특징적인 접촉 스케줄을 생성한다. 걷기(Walk)는 입각 다리 사이에 상당한 접촉 중첩(Contact Overlap)을 형성하며 일반적으로 지지가 완전히 사라지는 구간을 피한다. 트로트(Trot)는 대각선 지지 다리 쌍을 교대로 사용하고, 바운드(Bound)는 앞다리와 뒷다리 쌍을 교대로 사용한다. 캔터(Canter)와 갤럽(Gallop)은 특징적인 순서와 공중 구간(Aerial Phase)을 포함할 수 있는 비대칭 접촉 순서를 생성한다. 따라서 접촉 스케줄은 생물학적 명칭으로 정의된 보행을 명시적인 제어 제약조건으로 변환하는 공통 표현을 제공한다.

최적화 기반 이동(Optimization-Based Locomotion)에서는 일반적으로 접촉 스케줄을 유한한 예측 구간(Prediction Horizon)까지 확장한다. 각각의 미래 시간 단계에는 모든 발의 예상 접촉 상태가 포함되며, 이를 통해 접촉 테이블(Contact Table) 또는 접촉 행렬(Contact Matrix)이 생성된다. 모델 예측 제어(Model Predictive Control)는 이를 이용하여 각 예측 단계에서 어떤 발이 지면 반력을 생성할 수 있는지를 결정한다. 유각 상태의 발에는 접촉력이 0 또는 제한된 값으로 설정되고, 입각 상태의 발은 균형, 가속, 운동량 조절(Momentum Regulation)에 참여한다.

접촉 스케줄의 품질은 결과적으로 생성되는 움직임의 실현 가능성(Feasibility)에 큰 영향을 미친다. 큰 힘이 필요한 상황에서 지나치게 많은 접촉을 제거하는 스케줄은 목표 몸체 가속도를 실현할 수 없게 만들 수 있다. 지나치게 짧은 입각 구간은 비현실적으로 큰 최대 힘(Peak Force)을 요구할 수 있으며, 잘못된 시점의 이륙(Liftoff)은 안정성을 감소시킬 수 있다. 따라서 접촉 스케줄링(Contact Scheduling)은 로봇 질량, 액추에이터 성능, 마찰, 목표 속도, 몸체 운동량, 사용 가능한 착지 위치의 기하학적 조건을 함께 고려해야 한다.

명목 스케줄(Nominal Schedule)은 예측 가능한 지형에서는 유용하지만 실제 환경의 이동에서는 적응(Adaptation)이 필요하다. 지형 높이 오차, 장애물, 순응성(Compliance), 미끄러짐(Slipping), 충격 교란(Impact Disturbance), 상태 추정 불확실성(State-Estimation Uncertainty)으로 인해 실제 접촉 이벤트가 계획된 이벤트와 달라질 수 있다. 강건한 이동 시스템(Robust Locomotion System)은 모든 착지와 이륙이 정확히 명목 시간에 발생한다고 계속 가정하는 대신 이러한 차이를 감지하고 스케줄 또는 그 실행 과정을 수정해야 한다.

조기 접촉(Early Contact)은 유각 중인 발이 예정된 착지 시점보다 먼저 환경과 접촉하는 현상이다. 이는 일반적으로 지형이 예상보다 높거나 장애물이 계획된 유각 궤적(Swing Trajectory)과 교차할 때 발생한다. 제어기는 힘, 토크, 촉각(Tactile), 고유감각(Proprioceptive), 운동학적 정보를 이용하여 이러한 이벤트를 감지해야 한다. 상황에 따라 유각 운동을 종료하고 지지를 시작하며 새로운 물리적 상태를 반영하도록 접촉 스케줄을 갱신할 수 있다.

지연 접촉(Late Contact)은 계획된 착지 시간이 지났지만 발이 신뢰할 수 있는 지지를 확보하지 못한 경우에 발생한다. 지형의 함몰, 부정확한 고도 추정(Elevation Estimate), 위치 오차 등이 이러한 상태를 발생시킬 수 있다. 해당 발을 즉시 하중을 지지하는 접촉으로 처리하면 잘못된 힘이나 불안정한 명령이 발생할 수 있다. 대신 제어기는 유각 궤적을 아래쪽으로 연장하고 힘 활성화를 지연시키며, 접촉이 확인될 때까지 나머지 입각 다리를 이용하여 몸체를 지지할 수 있다.

따라서 접촉 감지(Contact Detection)는 스케줄 적응에서 핵심적인 역할을 한다. 관절 토크(Joint Torque), 모터 전류(Motor Current), 발 힘 센서(Foot Force Sensor), 관성 센서(Inertial Sensor), 촉각 장치(Tactile Device), 상태 추정기(State Estimator)의 측정값을 결합하여 발이 실제로 환경을 지지하고 있는지를 추정할 수 있다. 신뢰성 높은 감지 시스템은 지속적인 접촉과 순간적인 충격 또는 센서 잡음(Sensor Noise)을 구분해야 한다. 접촉과 비접촉 상태 사이에서 빠르게 전환되는 현상을 방지하기 위해 필터링(Filtering)과 히스테리시스(Hysteresis)가 사용되는 경우가 많다.

계획 접촉(Planned Contact)과 추정 접촉(Estimated Contact)의 구분은 중요하다. 계획 접촉은 보행 생성기가 의도하는 상태를 나타내는 반면, 추정 접촉은 로봇이 실제 물리적으로 경험하고 있는 상태를 나타낸다. 두 상태가 일치하면 명목 제어기(Nominal Controller)는 정상적으로 동작할 수 있다. 두 상태가 일치하지 않으면 감독 로직(Supervisory Logic)은 보행 위상을 수정할지, 힘 제약조건을 변경할지, 발 궤적을 조정할지, 또는 복구 행동(Recovery Behavior)을 실행할지를 결정해야 한다.

위상 적응(Phase Adaptation)은 접촉 타이밍 오차를 조정하는 한 가지 방법을 제공한다. 착지가 일찍 발생하면 해당 다리의 위상을 입각 구간 방향으로 앞당길 수 있다. 착지가 지연되면 위상 진행을 늦추거나 일시적으로 정지할 수 있다. 보다 정교한 방법에서는 전체 보행의 협응을 유지하기 위해 여러 다리의 위상을 함께 수정한다. 이를 통해 국부적인 접촉 보정이 네 다리 사이의 전체적인 타이밍 관계를 파괴하는 것을 방지할 수 있다.

스케줄 적응(Schedule Adaptation)은 또한 충분한 지지 상태를 유지해야 한다. 하나의 다리를 들어 올리기 전에 제어기는 나머지 접촉 다리만으로 목표 몸체 움직임을 지지할 수 있는지를 평가할 수 있다. 다른 다리가 접촉을 확보하지 못한 경우 예정된 이륙을 지연시킬 수 있다. 이러한 이벤트 기반 입각 연장(Event-Based Stance Extension)은 다른 지지가 물리적으로 확보되기 전에 안정적인 기존 지지를 무조건 제거하는 것을 방지하기 때문에 거친 지형에서 특히 유용하다.

착지 위치 계획(Foothold Planning)과 접촉 스케줄링(Contact Scheduling)은 밀접하게 결합되어 있다. 접촉 스케줄은 새로운 착지 위치가 언제 필요한지를 결정하고, 지형 인식(Terrain Perception)은 실현 가능한 착지 위치가 어디에 존재하는지를 결정한다. 예정된 착지 영역에 장애물, 구멍, 급경사 표면 또는 낮은 마찰 영역이 존재한다면 계획기는 착지 위치를 변경해야 할 수 있다. 착지 위치가 크게 변경되면 유각 지속 시간, 입각 지속 시간 또는 인접 다리의 타이밍도 함께 변경해야 할 수 있다.

지형 인식형 스케줄링(Terrain-Aware Scheduling)은 고도 지도(Elevation Map), 표면 법선(Surface Normal), 주행 가능성 추정(Traversability Estimate), 의미론적 정보(Semantic Information), 마찰 예측(Friction Prediction)을 활용할 수 있다. 어려운 지형에서는 더 긴 입각 중첩, 낮은 보행 주파수, 보수적인 접촉 전환이 유리할 수 있다. 반대로 평탄하고 예측 가능한 지면에서는 더 짧은 지지 구간을 사용하는 동적인 스케줄을 적용할 수 있다. 따라서 환경 인식은 로봇이 어디에 발을 디딜 것인지뿐만 아니라 각 접촉이 언제 발생해야 하는지에도 영향을 줄 수 있다.

목표 움직임(Desired Motion)은 또 다른 적응 신호를 제공한다. 가속, 감속, 회전 또는 횡방향 이동 과정에서는 정상적인 전진 이동에서 사용하는 것과 다른 접촉 패턴이 더 효과적일 수 있다. 제어기는 지지 발이 유리한 방향의 힘을 생성할 수 있도록 입각 지속 시간이나 접촉 타이밍을 수정할 수 있다. 따라서 상위 수준 명령(High-Level Command)은 공간적인 착지 위치 배치와 시간적인 접촉 구성 모두에 영향을 미친다.

외부 교란(External Disturbance)이 발생하면 명목 스케줄에서 빠르게 벗어나야 할 수 있다. 외력이 가해지면 무게중심(Center of Mass)이나 각운동량(Angular Momentum)이 현재 계획된 접촉만으로 복구할 수 있는 범위를 벗어날 수 있다. 로봇은 기존 입각을 연장하거나, 유각 중인 발을 더 일찍 착지시키거나, 추가적인 복구 발걸음(Recovery Step)을 도입하여 대응할 수 있다. 이러한 상황에서 접촉 스케줄링은 단순한 주기적 피드포워드 과정(Periodic Feedforward Process)이 아니라 피드백 안정화(Feedback Stabilization)의 일부가 된다.

접촉 스케줄 최적화(Contact Schedule Optimization)는 착지 및 이륙 시간을 고정된 보행 매개변수가 아니라 의사결정 변수(Decision Variable)로 취급할 수 있다. 궤적 최적화(Trajectory Optimization)는 동역학 및 마찰 제약조건을 만족시키면서 몸체 움직임, 발 배치, 접촉력, 접촉 타이밍을 동시에 결정할 수 있다. 이러한 접근법은 매우 효과적인 움직임을 발견할 수 있지만 접촉 모드의 변화가 동역학에 이산적(Discrete) 또는 하이브리드 구조(Hybrid Structure)를 도입하기 때문에 최적화 문제는 더욱 어려워진다.

하이브리드 이동 모델(Hybrid Locomotion Model)은 연속적인 움직임과 이산적인 접촉 전환의 조합을 명시적으로 표현한다. 하나의 접촉 모드 내부에서 로봇은 연속 동역학(Continuous Dynamics)에 따라 움직이며, 착지 또는 이륙 이벤트가 발생하면 다른 모드로 전환된다. 따라서 접촉 스케줄링은 이러한 하이브리드 모드의 순서와 지속 시간을 결정한다. 이러한 구조를 이해하는 것은 안정성을 분석하고 최적화 기반 제어, 모델 예측 제어, 이벤트 구동 제어기(Event-Driven Controller)를 설계하는 데 중요하다.

학습 기반 방법(Learning-Based Method)도 접촉 스케줄을 생성하거나 적응시킬 수 있다. 강화학습 정책(Reinforcement-Learning Policy)은 관절 동작을 통해 접촉 타이밍을 암묵적으로 학습할 수 있으며, 계층적 정책(Hierarchical Policy)은 목표 접촉 상태와 위상 매개변수를 명시적으로 출력할 수도 있다. 학습 기반 스케줄링은 복잡한 지형에 유연하게 대응할 수 있지만 물리적 제약조건은 여전히 필수적이다. 접촉력, 마찰 한계, 자기 충돌(Self-Collision), 액추에이터 한계, 최소 지지 요구조건은 하위 수준 제어기나 안전 계층(Safety Layer)을 통해 강제할 수 있다.

스케줄 적응(Schedule Adaptation)은 여러 시간 척도(Time Scale)에서 동작한다. 상위 수준의 보행 선택은 수백 밀리초에서 수 초 단위로 변경될 수 있는 반면, 착지 위치와 위상 조정은 개별 발걸음 내부에서 이루어진다. 접촉 감지와 충격 대응(Impact Response)은 이보다 훨씬 빠른 갱신이 필요할 수 있다. 따라서 실제 시스템 구조에서는 느린 전략적 적응(Strategic Adaptation)과 빠른 반응형 보정(Reactive Correction)을 분리하면서 계획 및 제어 계층 전체에서 일관된 접촉 표현을 유지한다.

접촉 스케줄은 상태 추정(State Estimation)에도 중요한 정보를 제공한다. 신뢰할 수 있는 입각 상태에서는 발이 환경에 대해 거의 정지되어 있다고 간주할 수 있으며, 이를 통해 몸체 속도와 자세를 추정하는 데 도움이 되는 운동학적 제약조건(Kinematic Constraint)을 제공할 수 있다. 잘못된 접촉 분류(Contact Classification)는 이러한 추정값을 손상시킬 수 있다. 따라서 접촉 추정, 상태 추정, 보행 제어는 서로 의존하며 완전히 독립된 모듈로 동작하기보다 신뢰도 정보(Confidence Information)를 상호 교환해야 한다.

고장 상태(Fault Condition)는 적응형 스케줄링의 중요성을 더욱 명확하게 보여준다. 하나의 다리에서 액추에이터 성능 저하, 센서 고장, 또는 하중 지지 능력 감소가 발생하면 이동 시스템은 해당 다리의 입각 힘 기여도를 줄이거나 주요 지지 다리로 사용하는 것을 피해야 할 수 있다. 나머지 다리에는 수정된 접촉 지속 시간과 힘 분배(Force Allocation)를 적용할 수 있다. 이를 통해 즉각적인 전체 이동 능력 상실 대신 성능이 저하되더라도 제어 가능한 이동(Degraded but Controlled Locomotion)을 유지할 가능성이 생긴다.

피지컬 AI(Physical AI)의 관점에서 접촉 스케줄 생성(Contact Schedule Generation)은 이동 의도(Locomotion Intent)를 물리적 세계와의 구조화된 상호작용(Structured Physical Interaction)으로 변환하는 과정이다. 적응(Adaptation)은 측정된 환경 이벤트가 계획된 상호작용을 수정할 수 있도록 피드백 루프(Feedback Loop)를 형성한다. 인식(Perception)은 지형과 접촉 조건을 식별하고, 예측(Prediction)은 미래의 지지 가능성을 평가하며, 제어(Control)는 힘과 움직임을 생성하고, 피드백은 예상된 물리적 이벤트와 실제 이벤트 사이의 차이를 지속적으로 보정한다.

따라서 유능한 4족 로봇은 접촉 스케줄(Contact Schedule)을 변경할 수 없는 고정 시간표가 아니라 동적인 계획(Dynamic Plan)으로 취급해야 한다. 명목 보행 위상(Nominal Gait Phase)은 효율적인 구조를 제공하지만 실제 착지, 지형 형상, 외부 교란, 이동 명령, 하드웨어 제약조건에 따라 그 구조를 온라인으로 수정할 수 있어야 한다. 스케줄 생성과 인식, 추정, 최적화, 전신 제어를 통합함으로써 로봇은 환경의 물리적 현실에 맞게 접촉을 적응시키면서도 협응된 이동(Coordinated Locomotion)을 유지할 수 있다.

## 03.04. Foothold Planning Swing Foot Trajectory [w/Code]

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

착지점 계획(Foothold Planning)은 4족 로봇(Quadruped)이 원하는 몸체 움직임을 동역학적으로 실현 가능하고 안정적으로 유지하면서 주변 지형과 호환되도록 각 발을 어디에 배치해야 하는지를 결정한다. 유각 발 궤적 생성(Swing-Foot Trajectory Generation)은 현재 접촉 위치에서 선택된 착지점까지 발이 어떻게 이동할지를 결정한다. 이 두 과정은 지형 인식(Terrain Perception)과 동작 계획(Motion Planning)을 보행 생성(Gait Generation), 접촉 스케줄링(Contact Scheduling), 전신 제어(Whole-Body Control), 물리적 상호작용(Physical Interaction)과 연결한다.

명목 착지점(Nominal Foothold)은 먼저 로봇의 목표 속도와 보행 타이밍(Gait Timing)을 이용하여 생성할 수 있다. 다음 입각 구간 동안 몸체가 전진할 것으로 예상된다면 일반적으로 발은 현재 몸체 기준 위치보다 앞쪽에 배치되어야 한다. 필요한 변위는 명령된 병진 속도(Translational Velocity), 요 회전율(Yaw Rate), 입각 지속 시간(Stance Duration), 몸체 형상(Body Geometry), 다리의 명목 구성(Nominal Configuration)에 따라 결정된다. 이는 지형 제약조건을 고려하기 전에 사용할 수 있는 기본 기준을 제공한다.

속도 피드백(Velocity Feedback)을 이용하면 이러한 명목 위치를 수정하여 추종 오차(Tracking Error)를 줄이고 몸체 운동량(Body Momentum)을 조절할 수 있다. 로봇이 명령된 속도보다 빠르게 움직이면 다음 착지점을 이동시켜 제동 효과를 발생시킬 수 있다. 반대로 너무 느리게 움직이면 추가적인 가속을 지원하도록 착지점을 조정할 수 있다. 이와 유사한 보정은 횡방향 속도나 요 오차(Yaw Error)를 보상할 수 있다. 따라서 발 배치(Foot Placement)는 단순히 개별 다리의 위치를 결정하는 것이 아니라 전신 움직임을 제어하는 중요한 메커니즘으로 기능한다.

동역학 모델(Dynamic Model)을 사용하면 더욱 체계적인 착지점 결정 규칙을 구성할 수 있다. 역진자 모델(Inverted-Pendulum Model)이나 중심 동역학 모델(Centroidal Model)과 같은 단순화된 표현은 무게중심(Center of Mass)의 움직임과 미래의 지지 위치 사이의 관계를 나타낸다. 캡처 포인트(Capture Point)와 유사한 개념은 불안정한 몸체 움직임을 조절하기 위해 지지를 어디에 형성해야 하는지를 추정한다. 보다 완전한 최적화 방법은 4족 로봇의 물리적 제약조건을 만족하면서 몸체 궤적, 각운동량(Angular Momentum), 접촉력(Contact Force), 착지점 위치를 동시에 고려한다.

명목 착지점은 해당 다리의 도달 가능한 작업 공간(Reachable Workspace) 내부에 위치해야 한다. 고관절 위치(Hip Location), 링크 길이(Link Length), 관절 한계(Joint Limit), 몸체 자세(Body Orientation), 입각 중 예상되는 몸체 움직임이 이러한 실현 가능 영역을 결정한다. 지형상으로 적합한 지점이라도 관절 제약조건을 위반하지 않고 다리가 도달할 수 없다면 사용할 수 없다. 따라서 실제 계획기는 착지점 후보를 선택하기 전에 지형 적합성(Terrain Suitability)과 운동학적 도달 가능성(Kinematic Reachability)을 함께 평가한다.

지형 인식(Terrain Perception)은 착지점 계획을 단순한 기하학적 타이밍 문제에서 환경 인식형 의사결정(Environment-Aware Decision) 문제로 확장한다. 고도 지도(Elevation Map), 깊이 측정(Depth Measurement), 포인트 클라우드(Point Cloud), 표면 법선(Surface Normal), 의미론적 레이블(Semantic Label), 주행 가능성 추정(Traversability Estimate)을 이용하여 지지 가능한 후보 영역을 식별할 수 있다. 계획기는 구멍, 장애물 모서리, 불안정한 물체, 지나치게 가파른 경사면, 그리고 형상이나 재질 특성으로 인해 신뢰할 수 있는 접촉이 어려운 표면을 피해야 한다.

착지점 품질(Foothold Quality)은 비용 함수(Cost Function)를 이용하여 표현할 수 있다. 후보 위치는 명목 착지점으로부터의 거리, 지형 경사(Terrain Slope), 표면 거칠기(Surface Roughness), 모서리까지의 거리, 추정 마찰(Estimated Friction), 운동학적 여유(Kinematic Margin), 예상 접촉력, 충돌 위험(Collision Risk)을 기준으로 평가할 수 있다. 계획기는 단순히 가장 가까우면서 기하학적으로 도달 가능한 지점을 선택하는 것이 아니라 이러한 요소들 사이에서 유리한 절충 관계를 제공하는 위치를 선택한다.

불확실성(Uncertainty) 역시 착지점 선택에 영향을 주어야 한다. 희소하거나 잡음이 많은 측정값으로 재구성된 지형 셀(Terrain Cell)은 평평하게 보이더라도 낮은 신뢰도를 가질 수 있다. 보수적인 계획(Conservative Planning)은 불확실한 영역에 불이익을 부여하거나 불연속 지형 주변의 안전 여유(Safety Margin)를 증가시킬 수 있다. 이는 깊이 카메라(Depth Camera)나 라이다(LiDAR)가 낮은 입사각으로 지형을 관측할 때 특히 중요하다. 이러한 조건에서는 가림(Occlusion)과 측정 잡음으로 인해 계단, 바위 또는 음의 장애물(Negative Obstacle) 주변에서 신뢰할 수 없는 추정이 발생할 수 있다.

착지점은 미래의 접촉 스케줄(Contact Schedule)도 지원해야 한다. 하나의 다리에 대해 유효한 위치가 다른 계획된 접촉과 함께 고려했을 때는 적절하지 않을 수 있다. 결합된 지지 형상(Support Geometry)은 전체 입각 구간에서 필요한 몸체 힘과 모멘트(Body Moment)를 생성할 수 있어야 한다. 따라서 고급 계획기는 여러 착지점을 함께 평가하거나 모델 예측 제어(Model Predictive Control) 또는 궤적 최적화(Trajectory Optimization)에 미래의 접촉 상태를 포함한다.

착지점이 선택되면 유각 발 궤적 생성(Swing-Foot Trajectory Generation)은 이륙(Liftoff)에서 착지(Touchdown)까지의 연속적인 경로를 정의한다. 궤적은 지형 위로 충분한 여유 높이(Clearance)를 확보하면서 위치와 속도의 경계조건(Boundary Condition)을 만족해야 한다. 간단한 궤적은 다항식 구간(Polynomial Segment), 스플라인(Spline), 베지어 곡선(Bézier Curve)을 이용하여 구성할 수 있다. 이러한 표현은 부드러운 미분 특성을 제공하며 소수의 직관적인 매개변수를 통해 궤적 형상을 수정할 수 있도록 한다.

일반적인 유각 궤적(Swing Trajectory)은 수평 이동과 수직 여유 높이를 분리하여 구성한다. 수평 좌표는 이륙 위치에서 목표 착지점으로 이동하고, 수직 좌표는 여유 높이까지 상승한 후 다시 지면 방향으로 하강한다. 최고점은 일반적으로 유각 중간 부근에서 형성되지만 높은 장애물 위로 올라가거나 높은 지형에서 낮은 지형으로 내려갈 때는 비대칭 궤적(Asymmetric Trajectory)이 더 적합할 수 있다.

지형 정보를 사용할 수 있다면 유각 높이(Swing Height)는 고정된 값이 아니라 적응적으로 조절되어야 한다. 지나치게 높은 여유 높이는 에너지를 낭비하고 더 높은 관절 속도를 요구하는 반면, 여유 높이가 부족하면 충돌 가능성이 증가한다. 지형 인식형 계획기(Terrain-Aware Planner)는 예상되는 발 이동 경로를 따라 고도 프로파일(Elevation Profile)을 확인하고 가장 높은 관련 장애물보다 위쪽에 불확실성 및 안전 여유를 추가하여 궤적을 설정할 수 있다.

발 가속도의 급격한 변화는 관절 토크와 몸체 교란으로 전달되기 때문에 궤적 평활성(Trajectory Smoothness)은 중요하다. 위치, 속도, 그리고 가능하면 가속도는 궤적 구간 사이에서 연속적으로 유지되어야 한다. 이륙 부근에서는 불필요한 충격량(Impulse)을 생성하지 않아야 하며, 착지 부근에서는 제어된 접촉을 준비하도록 궤적을 구성해야 한다. 부드러운 보간(Smooth Interpolation)은 기계적 응력을 감소시키고 하위 수준 관절 제어기의 궤적 추종 성능을 향상시킨다.

착지 속도(Touchdown Velocity)는 특히 중요한 설계 변수이다. 지나치게 큰 하향 속도는 높은 충격력을 발생시키고 구조적 진동(Structural Vibration)을 유발하며 미끄러짐이나 반발(Rebound)의 가능성을 증가시킬 수 있다. 반대로 지나치게 느린 접근은 접촉 타이밍을 불확실하게 만들 수 있다. 따라서 목표 착지 속도는 보행 속도, 지형 순응성(Terrain Compliance), 센싱 품질(Sensing Quality), 그리고 제어기의 충격 감지 및 조절 능력에 따라 선택된다.

로봇이 충분한 말단 자유도(Distal Degree of Freedom) 또는 관절형 발(Articulated Foot)을 가지고 있다면 발 자세(Foot Orientation)도 계획할 수 있다. 경사진 지형에서는 발을 추정된 표면 법선과 정렬함으로써 접촉 면적을 증가시키고 힘 전달을 개선할 수 있다. 점 접촉 발(Point Foot)을 사용하는 로봇에서는 발 자세를 직접 제어하지 못할 수 있지만 접근 방향과 다리 구성은 여전히 접촉 강건성(Contact Robustness)과 생성 가능한 마찰력에 영향을 준다.

유각 운동은 발뿐만 아니라 다리 전체에 대한 충돌 제약조건(Collision Constraint)을 만족해야 한다. 발 궤적이 장애물을 통과하더라도 정강이(Shin), 무릎(Knee), 또는 다른 링크가 지형이나 로봇 자체와 충돌할 수 있다. 따라서 고급 계획기는 스윕 체적(Swept Volume) 또는 구성 공간(Configuration Space)을 검사하며 충분한 여유를 유지하기 위해 무릎 자세, 유각 높이, 횡방향 움직임 또는 몸체 자세를 수정할 수 있다.

유각 과정에서 인식 정보가 변경되면 온라인 재계획(Online Replanning)이 필요하다. 새로운 지형 측정값을 통해 선택된 착지점이 안전하지 않거나 계획된 경로에 장애물이 존재한다는 사실이 발견될 수 있다. 착지까지 남은 시간이 제한되어 있기 때문에 재계획은 궤적의 연속성을 유지하면서 발을 새로운 실현 가능한 목표로 이동시켜야 한다. 남은 유각 시간과 액추에이터 한계는 착지점을 얼마나 멀리 변경할 수 있는지를 제한한다.

조기 접촉(Early Contact)은 유각 실행을 수정해야 하는 또 다른 원인이 된다. 발이 목표 위치에 도달하기 전에 지형과 충돌하면 명목 궤적을 계속 추종하는 것은 과도한 힘을 발생시키거나 로봇이 걸려 넘어지게 할 수 있다. 접촉 감지(Contact Detection)를 통해 유각 궤적을 종료하거나 수정하고 해당 다리를 입각 상태로 전환할 수 있다. 동시에 예상하지 못한 접촉은 인식된 표면 형상이 부정확했다는 직접적인 증거를 제공하므로 제어기는 지형 추정값을 갱신할 수 있다.

지연 접촉(Late Contact)은 발이 예상된 착지 영역에 도달했지만 지면과 접촉하지 못한 경우에 발생한다. 제어기는 하중 전달을 지연시키면서 제어된 탐색 궤적(Search Trajectory)을 이용하여 발을 아래쪽으로 연장할 수 있다. 이 과정에서 나머지 입각 다리는 몸체 지지를 유지해야 한다. 그래도 접촉을 형성할 수 없다면 다리가 무한정 지면을 탐색하도록 두는 대신 계획기가 다른 착지점을 선택하거나 복구 행동(Recovery Behavior)을 시작해야 할 수 있다.

회전(Turning)에서는 착지점 계획이 몸체의 회전 운동을 고려해야 한다. 각 발의 명목 위치는 선형 속도뿐만 아니라 요 회전율과 몸체 중심에 대한 해당 발의 상대 위치에도 영향을 받는다. 회전 중에는 안쪽 다리와 바깥쪽 다리가 서로 다른 공간 경로를 따른다. 적절한 발 배치는 과도한 다리 교차, 관절 한계 위반, 원하지 않는 횡방향 힘을 방지하면서 로봇이 회전에 필요한 모멘트를 생성할 수 있도록 한다.

고속 이동(High-Speed Locomotion)은 착지점 정확도에 더 높은 요구조건을 부여한다. 짧은 입각 시간은 착지 이후 몸체 운동량을 보정할 수 있는 기회를 감소시키며, 높은 속도는 발 배치 오차의 영향을 증폭시킨다. 계획기는 예측 지연(Prediction Latency), 상태 추정 불확실성, 액추에이터 응답, 지형 형상을 고려해야 한다. 따라서 동적 보행(Dynamic Gait)은 순수한 반응형 보정보다 예측 기반 발 배치(Predictive Foot Placement)에 의존하는 경우가 많다.

최적화 기반 접근법(Optimization-Based Approach)은 착지점과 유각 궤적 변수를 동시에 계산할 수 있다. 목적 함수(Objective Function)는 추종 오차, 에너지 사용량, 충격 속도, 지형 위험도, 명목 착지점으로부터의 편차, 운동학적 한계에 대한 근접도를 최소화하도록 구성할 수 있다. 제약조건은 도달 가능성, 충돌 회피, 접촉 실현 가능성, 마찰 한계, 액추에이터 성능을 보장한다. 이러한 최적화는 높은 유연성을 제공하지만 온라인 이동에 사용할 수 있을 정도의 계산 효율성을 확보해야 한다.

학습 기반 방법(Learning-Based Method)은 지형 관측과 로봇 상태를 이용하여 착지점 보정이나 유각 매개변수를 예측함으로써 해석적 계획(Analytical Planning)을 보완할 수 있다. 강화학습(Reinforcement Learning)은 수작업으로 설계하기 어려운 발걸음 전략을 발견할 수 있으며, 모방학습(Imitation Learning)은 전문가의 이동 행동을 재현할 수 있다. 안전 및 실현 가능성 계층(Safety and Feasibility Layer)은 학습된 출력을 제한하여 명령된 착지점이 도달 가능한 범위에 유지되고 유각 궤적이 알려진 위험 요소를 회피하도록 할 수 있다.

착지점 계획과 유각 제어는 인식(Perception)과 피지컬 AI(Physical AI)를 연결하는 자연스러운 연결점을 제공한다. 지형 관측값은 물리적인 지지가 어디에서 안전하게 형성될 수 있는지에 대한 실행 가능한 가설(Actionable Hypothesis)로 변환된다. 이후 로봇은 자유 공간(Free Space)을 통해 다리를 이동시키고 접촉을 통해 환경을 시험함으로써 이러한 가설 가운데 하나를 실제 행동으로 선택한다. 따라서 착지는 제어 이벤트(Control Event)이면서 동시에 새로운 물리적 정보를 획득하는 과정이 된다.

따라서 강건한 4족 로봇 이동 시스템(Robust Quadruped Locomotion System)은 착지점 선택과 유각 발 궤적 생성을 서로 결합되고 지속적으로 갱신되는 과정으로 다루어야 한다. 목표 몸체 움직임은 명목 발걸음을 제안하고, 인식은 실현 가능한 지형을 식별하며, 동역학은 유용한 지지 위치를 결정하고, 궤적 생성은 각 발을 안전하게 접촉 위치로 이동시킨다. 예상하지 못한 충돌이나 지면 부재에 대한 피드백은 실행 과정과 미래 계획을 다시 갱신하며, 이를 통해 예측(Prediction)과 물리적 상호작용 사이의 폐루프(Closed Loop)가 형성된다.

## 03.05. Gait Transition Smooth Mode Switching [w/Code]

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

보행 전환(Gait Transition)은 균형(Balance), 실현 가능한 접촉력(Contact Force), 연속적인 몸체 움직임(Body Motion), 협응된 다리 타이밍(Limb Timing)을 유지하면서 4족 로봇(Quadruped)을 하나의 이동 패턴에서 다른 이동 패턴으로 변경하는 과정이다. 대표적인 전환에는 걷기에서 트로트(Walk-to-Trot), 트로트에서 바운드(Trot-to-Bound), 또는 동적 이동에서 정적 이동(Dynamic-to-Static Motion)으로의 전환이 있다. 단순한 모드 교체와 달리 부드러운 전환(Smooth Switching)은 초기 보행과 목표 보행 사이에서 나타나는 일시적인 접촉 패턴과 동적 상태를 관리해야 한다.

각각의 보행(Gait)은 위상 오프셋(Phase Offset), 듀티 팩터(Duty Factor), 주기 주파수(Cycle Frequency), 입각 지속 시간(Stance Duration), 유각 지속 시간(Swing Duration), 보폭 길이(Stride Length), 접촉 순서(Contact Sequence)와 같은 매개변수로 설명할 수 있다. 따라서 보행 전환은 이러한 매개변수 공간(Parameter Space)의 한 영역에서 다른 영역으로 이동하는 과정이다. 이러한 매개변수를 갑작스럽게 변경하면 발이 예상하지 못한 시점에 들어 올려지거나 접촉력이 지나치게 빠르게 사라질 수 있으며, 명령된 관절 움직임이 불연속적으로 변화하여 불안정성이나 큰 기계적 하중을 발생시킬 수 있다.

가장 기본적인 요구조건은 접촉 일관성(Contact Consistency)이다. 현재 상당한 몸체 하중을 지지하고 있는 다리가 목표 보행에서 다른 위상을 갖는다는 이유만으로 갑자기 유각 다리로 분류되어서는 안 된다. 접촉을 해제하기 전에 나머지 다리들이 필요한 몸체 힘과 모멘트(Body Force and Moment)를 지지할 수 있어야 한다. 따라서 전환 로직(Transition Logic)은 단순히 경과 시간에 의존하는 것이 아니라 실제 착지(Touchdown), 이륙(Liftoff), 하중 전달(Load Transfer) 이벤트와 위상 변화를 협응시킨다.

위상 정렬(Phase Alignment)은 보행 전환을 시작하기 위한 실용적인 메커니즘을 제공한다. 제어기는 현재 보행이 목표 보행과 호환 가능한 구성에 도달할 때까지 기다린 후 위상 관계를 변경하기 시작할 수 있다. 예를 들어 걷기에서 트로트로 전환할 때는 대각선 다리들이 자연스럽게 쌍을 이루는 움직임으로 발전할 수 있는 타이밍 관계에 접근했을 때 전환을 시작할 수 있다. 유리한 전환 위상(Transition Phase)을 선택하면 각 다리에 필요한 시간적 보정의 크기를 줄일 수 있다.

이후 위상 오프셋(Phase Offset)을 초기값에서 목표 보행의 값으로 보간(Interpolation)할 수 있다. 직접적인 선형 보간(Linear Interpolation)은 개념적으로 단순하지만 위상은 주기적이므로 주기 경계 부근에서 주의하여 처리해야 한다. 원형 보간(Circular Interpolation)이나 오실레이터 기반 동기화(Oscillator-Based Synchronization)를 사용하면 인위적인 위상 점프를 방지할 수 있다. 또한 전환 속도는 사용 가능한 입각 및 유각 시간을 고려해야 하며, 새로운 위상 관계를 만족시키기 위해 특정 다리가 비현실적으로 빠르게 가속하도록 만들어서는 안 된다.

듀티 팩터(Duty Factor)는 느린 보행과 동적 보행 사이에서 크게 변화하는 경우가 많다. 걷기(Walk)는 일반적으로 긴 입각 구간과 높은 접촉 중첩(Contact Overlap)을 사용하는 반면, 달리기 계열 보행(Running Gait)은 입각 시간을 단축하고 공중 구간(Aerial Phase)을 포함할 수 있다. 듀티 팩터를 지나치게 빠르게 감소시키면 몸체 운동량이 동적 이동에 적합한 상태가 되기 전에 지지를 잃을 수 있다. 부드러운 전환에서는 제어기가 지면 반력(Ground Reaction Force)과 몸체 궤적을 동시에 재구성하면서 입각과 유각의 타이밍을 점진적으로 조절한다.

주기 주파수(Cycle Frequency) 역시 중요한 전환 변수이다. 속도를 높이려면 일반적으로 발걸음 주파수를 증가시켜야 하지만, 주파수를 순간적으로 변경하면 위상 진행과 발 타이밍이 갑작스럽게 변한다. 대신 여러 발걸음에 걸쳐 주파수를 목표값까지 점진적으로 증가시킬 수 있다. 변화율은 액추에이터 성능, 목표 가속도, 지형 품질, 현재 동적 안정성(Dynamic Stability)에 따라 결정될 수 있으며, 이를 통해 과도한 관절 움직임을 발생시키지 않고 이동 리듬을 가속할 수 있다.

보폭 길이(Stride Length)는 주파수와 명령 속도(Commanded Velocity)에 맞추어 일관되게 변화해야 한다. 주파수가 증가하는 동안 보폭 길이가 일시적으로 그대로 유지되면 로봇이 의도한 것보다 빠르게 가속할 수 있다. 반대로 보폭을 너무 일찍 줄이면 제동 효과가 발생할 수 있다. 따라서 전환 관리(Transition Management)는 시간적 보행 매개변수와 공간적 발 배치 매개변수(Spatial Foot-Placement Parameter)를 협응시켜 몸체 속도가 갑작스럽게 변하지 않고 부드러운 궤적을 따르도록 한다.

몸체 궤적 연속성(Body Trajectory Continuity)은 다리 타이밍만큼 중요하다. 서로 다른 보행은 서로 다른 선호 몸체 높이, 피치 진동(Pitch Oscillation), 수직 무게중심 운동(Vertical Center-of-Mass Motion), 각운동량 패턴(Angular Momentum Pattern)을 가질 수 있다. 기준 궤적(Reference Trajectory)을 갑작스럽게 전환하면 큰 제어 오차가 발생할 수 있다. 부드러운 모드 전환은 몸체 위치, 속도, 자세, 운동량 기준값을 혼합하여 전신 제어기(Whole-Body Controller)가 전환 과정 전체에서 동역학적으로 호환 가능한 명령을 받도록 한다.

지면 반력 재분배(Ground Reaction Force Redistribution)는 성공적인 하중 전달의 핵심이다. 전환 중에는 입각 상태에서 벗어나는 다리의 접촉력을 계속 입각 상태를 유지하거나 새롭게 입각 상태로 진입하는 다리로 점진적으로 이동시켜야 한다. 갑작스러운 힘 제거는 몸체 가속이나 회전을 발생시킬 수 있으며, 갑작스러운 힘 적용은 충격을 유발할 수 있다. 최적화 기반 제어기(Optimization-Based Controller)는 힘 변화율(Force Rate)을 명시적으로 조절하고 마찰, 토크, 접촉 제약조건에 따라 하중을 분배할 수 있다.

공중 구간을 포함하는 보행(Aerial Gait)으로의 전환은 안정화 메커니즘 자체가 근본적으로 변화하기 때문에 특별한 주의가 필요하다. 걷기 상태의 로봇은 연속적인 지면 지지에 크게 의존할 수 있지만, 달리기나 바운드 상태의 로봇은 지면과 접촉하지 않는 구간을 견뎌야 한다. 공중 구간에 진입하기 전에 로봇은 적절한 선운동량(Linear Momentum)과 각운동량(Angular Momentum)을 확보해야 한다. 따라서 비행(Flight) 직전의 마지막 입각은 예상되는 착지 구성과 힘 프로파일을 협응해야 하는 발사 이벤트(Launch Event)가 된다.

동적 보행에서 느린 보행으로 전환할 때는 반대의 문제가 발생한다. 접촉 중첩과 지지 지속 시간을 점진적으로 증가시키면서 과도한 운동에너지(Kinetic Energy)를 소산해야 한다. 제어기는 전방 착지 위치를 짧게 조정하고 제동력을 증가시키며 몸체 자세를 변경하는 동시에 주기 주파수를 감소시킬 수 있다. 고속 달리기 상태에서 정적 지지 패턴으로 직접 전환하려고 하면 마찰 또는 액추에이터 한계를 초과하여 미끄러짐이나 피칭(Pitching)을 발생시킬 수 있다.

회전 전환(Turning Transition)은 로봇이 회전하는 동안 보행 대칭성(Gait Symmetry)도 변경해야 할 수 있기 때문에 추가적인 복잡성을 가진다. 안쪽 다리와 바깥쪽 다리는 서로 다른 보폭을 필요로 하며 경우에 따라 서로 다른 타이밍도 필요하다. 직선 트로트에서 급격한 회전으로 전환하는 제어기는 일시적으로 비대칭적인 위상이나 착지점 패턴을 사용할 수 있다. 따라서 부드러운 전환에서는 목표 보행이 기동 과정 전체에서 완벽한 주기성을 유지하도록 강제하기보다 제어된 비대칭성(Controlled Asymmetry)을 허용해야 한다.

지형 조건(Terrain Condition)은 보행 전환이 안전하게 수행될 수 있는 시점을 결정할 수 있다. 속도 기반 제어기는 일반적으로 특정 속도 임계값 이상에서 걷기에서 트로트로 전환할 수 있지만, 거칠거나 미끄럽거나 불확실한 지형에서는 높은 듀티 팩터를 가진 보행을 유지해야 할 수 있다. 따라서 전환 로직은 명령 속도만을 전환 변수로 사용하는 대신 지형 경사, 거칠기, 마찰 추정(Friction Estimate), 착지점 가용성(Foothold Availability), 인식 신뢰도(Perception Confidence)를 함께 고려해야 한다.

보행 선택이 임계값에 따라 결정되는 경우 히스테리시스(Hysteresis)가 유용하다. 히스테리시스가 없으면 속도가 전환 경계 주변에서 변동할 때 걷기와 트로트 사이의 전환이 반복적으로 발생할 수 있다. 특정 보행에 진입할 때와 벗어날 때 서로 다른 임계값을 사용하면 이러한 모드 채터링(Mode Chattering)을 줄일 수 있다. 최소 유지 시간(Minimum Dwell Time)이나 전환 완료 조건을 추가하면 현재 전환이 동역학적으로 일관된 상태에 도달하기 전에 새로운 전환 요청이 발생하는 것을 방지할 수 있다.

유한 상태 기계(Finite-State Machine)는 보행 전환을 구현하는 간단한 방법을 제공한다. 각각의 상태는 안정적인 보행이나 중간 전환 모드를 나타내고, 속도 임계값, 발 접촉, 위상 조건과 같은 이벤트가 상태 변화를 발생시킨다. 이러한 구조는 해석하기 쉽고 검증하기도 용이하다. 그러나 보행 조합의 수가 증가하면 많은 전환 상태가 필요하게 되므로 고급 이동 시스템에서는 보다 연속적인 매개변수 기반 접근법(Parameter-Based Approach)이 유리할 수 있다.

연속 보행 다양체(Continuous Gait Manifold)는 이산적인 전환에 대한 대안을 제공한다. 걷기, 트로트, 바운드 및 중간 패턴을 공통 매개변수 공간의 서로 다른 영역으로 표현하면 제어기는 이들 사이를 연속적으로 이동할 수 있다. 위상 오프셋, 듀티 팩터, 주파수, 보폭 형상(Stride Geometry)은 부드럽게 변화하는 변수가 된다. 이러한 접근법에서는 보행 변경 자체가 매개변수 공간에서 하나의 궤적이 되기 때문에 보행 선택과 보행 전환 사이의 구분이 감소한다.

중앙 패턴 생성기(Central Pattern Generator)와 결합 오실레이터(Coupled Oscillator)는 부드러운 전환을 위한 또 다른 프레임워크를 제공한다. 각각의 다리를 다른 다리들과 위상 및 주파수가 결합된 하나의 오실레이터와 연결할 수 있다. 결합 관계나 오실레이터 매개변수를 변경하면 네트워크가 새로운 협응 패턴으로 수렴한다. 위상이 연속적으로 변화하기 때문에 이러한 시스템은 접촉 테이블(Contact Table)을 직접 교체할 때 발생할 수 있는 일부 불연속성을 자연스럽게 방지할 수 있다.

모델 예측 제어(Model Predictive Control)는 미래의 접촉 모드를 예측하고 전환 구간 전체에서 몸체 움직임과 접촉력을 최적화함으로써 보행 전환을 처리할 수 있다. 예측 구간(Prediction Horizon)은 현재 보행과 목표 보행 패턴을 모두 포함할 수 있다. 이를 통해 제어기는 미래의 지지 변화가 실제로 발생하기 전에 이를 예측하여 대응할 수 있다. 그러나 특히 접촉 타이밍 자체까지 최적화하는 경우 계획된 접촉 순서는 계산적으로 관리 가능한 수준을 유지해야 한다.

궤적 최적화(Trajectory Optimization)는 사전에 정의된 보간 규칙에 전적으로 의존하지 않고 동역학적으로 실현 가능한 전환을 탐색할 수 있다. 최적화기는 두 보행 상태를 연결하는 중간 착지점, 접촉 지속 시간, 힘 프로파일, 몸체 궤적을 결정할 수 있다. 이러한 방법은 속도나 운동량이 크게 변화하는 전환에서 특히 유용하지만 계산 비용으로 인해 고주파 온라인 제어(High-Frequency Online Control)에 직접 적용하는 데 제한이 있을 수 있다.

학습 기반 제어기(Learning-Based Controller)는 강화학습(Reinforcement Learning) 또는 모방학습(Imitation Learning)을 통해 보행 전환을 습득할 수 있다. 목표 속도나 보행 명령에 조건화된 정책(Conditioned Policy)은 명시적으로 설계된 전환 상태 없이도 협응 패턴을 변경하는 방법을 학습할 수 있다. 커리큘럼 학습(Curriculum Training)을 통해 정책에 점진적으로 더 큰 명령 변화를 경험시킬 수 있다. 그러나 시각적으로 부드러운 전환이 자동으로 동역학적으로 안전하거나 실제 하드웨어와 호환되는 것은 아니므로 제약조건과 검증이 여전히 필요하다.

모든 전환 과정에서 접촉 피드백(Contact Feedback)은 계속 활성화되어야 한다. 예상하지 못한 조기 착지(Early Touchdown)나 지연 착지(Late Touchdown)는 특히 불규칙한 지형에서 계획된 위상 보간을 무효화할 수 있다. 전환 관리자(Transition Manager)는 측정된 접촉 이벤트에 따라 예정된 이륙을 지연시키거나 입각을 연장하거나 위상을 다시 동기화할 수 있다. 이러한 이벤트 기반 보정(Event-Driven Correction)은 수학적으로 부드러운 매개변수 전환이 실제 환경과 물리적으로 불일치하는 상황을 방지한다.

액추에이터 한계(Actuator Limit)는 전환 속도에 추가적인 제약조건을 부여한다. 보행을 빠르게 변경하면 발 궤적이 기하학적으로 부드럽게 보이더라도 높은 관절 가속도, 토크 또는 동력(Power)을 요구할 수 있다. 열 상태(Thermal State)와 배터리 출력 역시 사용 가능한 성능을 제한할 수 있다. 따라서 실제 전환 관리자는 목표 보행에 얼마나 빠르게 도달할 수 있는지를 결정할 때 토크, 속도, 동력, 온도 여유(Thermal Margin)를 고려해야 한다.

안정성 평가(Stability Assessment)는 요청된 전환을 허용하거나 거부하는 데 사용할 수 있다. 보행 속도에 따라 지지 형상(Support Geometry), 무게중심 상태(Center-of-Mass State), 캡처 포인트(Capture Point)와 유사한 지표, 예측 접촉 실현 가능성(Predicted Contact Feasibility), 마찰 여유(Friction Margin), 중심 운동량(Centroidal Momentum) 등을 평가할 수 있다. 목표 보행으로 안전하게 진입할 수 없다면 제어기는 요청된 모드를 무조건 실행하는 대신 전환을 지연하거나 중간 보행(Intermediate Gait)을 선택할 수 있다.

피지컬 AI(Physical AI)의 관점에서 보행 전환은 체화된 의사결정(Embodied Decision Making)을 명확하게 보여주는 사례이다. 가속, 감속, 빠른 회전 또는 거친 지형 진입과 같은 상위 수준 의도(High-Level Intention)는 접촉, 운동량, 다리 협응의 물리적으로 실현 가능한 변화 순서로 변환되어야 한다. 인식(Perception)과 상태 추정(State Estimation)은 환경과 로봇 상태가 이러한 변화를 허용하는지를 판단하며, 제어(Control)는 그 결과 발생하는 물리적 영향을 지속적으로 관리한다.

따라서 부드러운 모드 전환(Smooth Mode Switching)은 하나의 보행 매개변수만을 보간하는 것 이상의 처리를 요구한다. 위상 관계, 듀티 팩터, 주파수, 착지점(Foothold), 몸체 궤적, 접촉력, 실제 접촉 이벤트가 운동학적 및 동역학적 제약조건 아래에서 일관되게 변화해야 한다. 보행 전환을 서로 다른 이동 영역(Locomotion Regime) 사이의 제어된 궤적(Controlled Trajectory)으로 다룸으로써 4족 로봇은 안정성, 기계적 안전성(Mechanical Safety), 환경과의 상호작용 연속성을 유지하면서 행동을 변경할 수 있다.

## 03.06. Trot Controller MPC Based Implementation [w/Code]

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

MPC 기반 트로트 제어기(MPC-Based Trot Controller)는 모델 예측 제어(Model Predictive Control)를 사용하여 유한한 예측 구간(Prediction Horizon)에서 몸체 움직임, 지면 반력(Ground Reaction Force), 교대로 전환되는 대각선 접촉(Diagonal Contact)을 협응한다. 현재의 추종 오차에만 반응하는 대신 MPC는 후보 제어 입력이 미래의 로봇 상태에 어떤 영향을 미칠지를 예측한다. 이러한 예측 구조는 대각선 다리 쌍 사이에서 지지가 빠르게 전환되고 각 전환 과정에서 동적 균형(Dynamic Balance)을 유지해야 하는 트로트(Trot)에 특히 유용하다.

명목 트로트(Nominal Trot)는 네 다리를 두 개의 대각선 다리 쌍으로 구분한다. 일반적으로 왼쪽 앞다리(Front-Left)와 오른쪽 뒷다리(Rear-Right)가 하나의 접촉 위상을 공유하고, 오른쪽 앞다리(Front-Right)와 왼쪽 뒷다리(Rear-Left)가 반대쪽 다리 쌍을 형성한다. 두 다리 쌍은 약 반 보행 주기(Half Gait Cycle)의 차이를 두고 교대로 움직인다. 듀티 팩터(Duty Factor)와 명령 속도에 따라 다리 쌍 사이의 전환에는 중첩 지지(Overlapping Support) 또는 짧은 공중 구간(Aerial Interval)이 포함될 수 있으며, 이는 MPC 문제에 적용되는 동적 제약조건(Dynamic Constraint)을 직접적으로 변화시킨다.

제어기(Controller)는 일반적으로 상위 수준 명령 계층(High-Level Command Layer)으로부터 목표 선속도(Desired Linear Velocity), 요 회전율(Yaw Rate), 몸체 높이(Body Height), 자세(Orientation)를 입력받는다. 보행 생성기(Gait Generator)는 목표 이동 모드(Locomotion Mode)를 위상 변수와 미래 접촉 스케줄(Future Contact Schedule)로 변환한다. 상태 추정(State Estimation)은 몸체 위치, 속도, 자세, 각속도(Angular Velocity), 관절 상태, 추정된 발 접촉 정보를 제공한다. 지형 정보는 추가적으로 국부 표면 높이, 법선 방향(Normal Direction), 마찰 추정(Friction Estimate), 실현 가능한 착지점 영역(Feasible Foothold Region)을 제공할 수 있다.

계산 효율성을 위해 예측 모델(Predictive Model)은 전체 관절 공간 동역학(Full Joint-Space Dynamics)보다 중심 동역학(Centroidal Dynamics) 또는 단일 강체 동역학(Single-Rigid-Body Dynamics)을 이용하여 로봇을 표현하는 경우가 많다. 몸체는 위치, 자세, 선운동량(Linear Momentum), 각운동량(Angular Momentum)을 갖는 하나의 강체 질량으로 근사된다. 입각 발에서 작용하는 지면 반력은 병진 가속도(Translational Acceleration)와 몸체 모멘트(Body Moment)를 생성한다. 이러한 축소 모델(Reduced Model)은 지배적인 전신 거동을 표현하면서도 실시간 최적화에 적합한 계산량을 유지한다.

병진 동역학(Translational Dynamics)은 전체 외력과 무게중심 가속도(Center-of-Mass Acceleration) 사이의 관계를 따른다. 모든 활성 접촉(Active Contact)에서 발생하는 지면 반력을 중력과 함께 합산하여 미래의 선형 움직임을 예측한다. 회전 동역학(Rotational Dynamics)은 발 접촉력과 그 모멘트 암(Moment Arm)을 각가속도(Angular Acceleration) 또는 각운동량과 연결한다. 따라서 각각의 입각 발이 무게중심에 대해 위치하는 상대적인 지점은 접촉력이 몸체의 롤(Roll), 피치(Pitch), 요(Yaw)를 얼마나 효과적으로 제어할 수 있는지를 결정한다.

비선형 예측 동역학(Nonlinear Predictive Dynamics)은 높은 주파수에서 최적화 문제를 풀 수 있도록 선형화(Linearization) 또는 이산화(Discretization)되는 경우가 많다. 상태 벡터(State Vector)와 제어 벡터(Control Vector)는 여러 미래 시간 단계에 걸쳐 전파된다. 구성 방식에 따라 최적화기는 이차 계획법(Quadratic Programming), 순차 이차 계획법(Sequential Quadratic Programming), 또는 비선형 계획법(Nonlinear Programming)을 사용할 수 있다. 실시간 4족 로봇 시스템에서는 충분한 동역학 정확도를 유지하면서도 예측 가능한 계산 시간을 제공하는 구성이 일반적으로 선호된다.

접촉 스케줄(Contact Schedule)은 각 예측 단계에서 어떤 지면 반력을 사용할 수 있는지를 결정한다. 입각 다리에는 힘 의사결정 변수(Force Decision Variable)가 할당되고, 유각 다리는 지지력을 생성하지 않도록 제한된다. 트로트에서는 계획된 위상에 따라 이러한 제약조건이 두 대각선 다리 쌍 사이에서 교대로 적용된다. 미래의 접촉 전환(Contact Switch)을 예측 구간 안에 포함함으로써 MPC는 실제 지지 전환이 발생하기 전에 몸체 상태를 미리 준비할 수 있다.

목적 함수(Objective Function)는 원하는 이동 거동을 정의한다. 일반적으로 몸체 위치, 선속도, 자세, 각속도 또는 운동량과 각각의 기준값 사이의 오차를 최소화하는 항이 포함된다. 추가적인 항을 사용하여 과도한 접촉력이나 급격한 힘 변화를 제한할 수 있다. 가중치 선택(Weight Selection)은 제어기가 속도 추종(Velocity Tracking), 자세 안정화(Attitude Stabilization), 부드러운 구동(Smooth Actuation), 에너지 관련 목표 가운데 무엇을 얼마나 중요하게 고려하는지를 결정하며, 결과적으로 생성되는 트로트의 특성에 큰 영향을 미친다.

접촉력(Contact Force)은 물리적 제약조건을 만족해야 한다. 일반적인 지면에서는 발이 지면을 당길 수 없기 때문에 법선력(Normal Force)은 일반적으로 압축 방향을 유지해야 한다. 접선력(Tangential Force)은 예측된 접촉이 미끄러지지 않도록 마찰 원뿔(Friction Cone)의 근사 영역 내부에 있어야 한다. 최대 힘 제한(Maximum Force Limit)은 액추에이터 성능, 구조적 하중 또는 지면의 지지 강도를 반영할 수 있다. 이러한 제약조건은 최적화기가 물리적으로 불가능한 접촉력을 사용하여 모델을 안정화하는 것을 방지한다.

MPC 예측 구간(Prediction Horizon)은 의미 있는 미래의 지지 전환을 포함할 수 있을 정도로 충분히 길어야 한다. 예측 구간이 현재의 대각선 입각 상태만 포함한다면 제어기는 다음 접촉 다리 쌍을 충분히 예측하지 못할 수 있다. 긴 예측 구간은 예측 능력을 향상시키지만 계산 비용과 모델 불확실성(Model Uncertainty)을 증가시킨다. 따라서 예측 구간 길이, 이산화 시간 간격(Discretization Interval), 솔버 주파수(Solver Frequency)는 보행 주기, 사용 가능한 계산 자원, 요구되는 제어 대역폭(Control Bandwidth)에 맞추어 함께 결정해야 한다.

각 MPC 갱신(Update)에서 최적화는 가장 최근에 추정된 로봇 상태에서 시작한다. 솔버(Solver)는 미래 접촉력의 최적 순서를 계산하지만 실제로는 그중 첫 번째 부분만 로봇에 적용한다. 다음 갱신 시점에는 새로운 측정값을 반영하여 최적화 문제를 다시 계산한다. 이러한 이동 예측 구간 메커니즘(Receding-Horizon Mechanism)은 피드백을 제공하며 제어기가 예측 오차, 외부 교란(Disturbance), 명목 트로트에서의 편차를 지속적으로 보정할 수 있도록 한다.

MPC는 일반적으로 가장 낮은 수준의 토크 제어기(Torque Controller)보다 낮은 주파수에서 동작한다. 최적화된 접촉력과 몸체 기준값은 전신 제어기(Whole-Body Controller), 역동역학 제어기(Inverse-Dynamics Controller), 또는 힘-토크 변환 계층(Force-to-Torque Mapping Layer)으로 전달된다. 다리 자코비안(Leg Jacobian)을 사용하면 목표 발 힘을 근사적으로 관절 토크로 변환할 수 있다. 보다 완전한 전신 제어 구성에서는 몸체 작업, 입각 제약조건, 유각 발 추종, 관절 한계를 동시에 만족시킨다.

유각 다리(Swing Leg)는 별도의 제어 과정이 필요하지만 MPC와 협응되어야 한다. MPC가 입각력을 통해 몸체 거동을 결정하는 동안 착지점 계획기(Foothold Planner)는 각 유각 다리의 다음 착지 위치를 선택한다. 목표 속도, 몸체 상태, 요 움직임, 지형 형상, 예측된 입각 타이밍이 목표 착지점에 영향을 준다. 이후 유각 궤적 생성기(Swing Trajectory Generator)는 충분한 지형 여유 높이(Terrain Clearance)와 적절한 착지 속도(Touchdown Velocity)를 갖는 부드러운 경로를 생성한다.

발 배치(Foot Placement)는 힘 제어만으로 이루어지는 안정화 외에도 트로트를 안정화하는 중요한 메커니즘을 제공한다. 몸체에 과도한 전진 속도가 발생하면 다음 착지점을 이동시켜 보정 제동 효과(Corrective Braking Effect)를 만들 수 있다. 횡방향 오차와 회전 오차도 이와 유사하게 처리할 수 있다. MPC는 미래의 몸체 움직임을 예측하므로 순간적인 속도 오차만 사용하는 대신 예측된 상태 정보를 이용하여 착지 위치를 정교하게 수정할 수 있다.

상태 추정(State Estimation)의 품질은 제어기 성능에 큰 영향을 미친다. 몸체 자세, 속도 또는 접촉 상태에 오차가 발생하면 잘못된 예측과 그에 따른 잘못된 최적 접촉력이 생성된다. 관성 측정 장치(Inertial Measurement Unit), 관절 엔코더(Joint Encoder), 접촉 센싱(Contact Sensing), 운동학적 제약조건(Kinematic Constraint), 그리고 경우에 따라 비전 또는 라이다 오도메트리(Visual or LiDAR Odometry)를 융합하여 로봇 상태를 추정한다. 신뢰할 수 있는 입각 상태에서는 발이 정지되어 있다는 가정(Stationary-Foot Assumption)을 이용하여 몸체 속도 드리프트를 줄이는 데 유용한 정보를 얻을 수 있다.

접촉 추정(Contact Estimation)은 계획된 입각(Planned Stance)과 실제 물리적 지지(Physical Support)를 구분해야 한다. 지형 높이 오차로 인해 발이 예상보다 일찍 또는 늦게 착지할 수 있다. 실제 접촉이 존재하기 전에 계획된 MPC 힘을 적용하는 것은 물리적으로 의미가 없으며, 예상하지 못한 접촉 이후에도 유각 제어를 계속하면 충격을 발생시킬 수 있다. 따라서 실제 구현에서는 접촉 피드백을 이용하여 힘 활성화(Force Activation)를 수정하고, 위상을 갱신하거나, 계획된 접촉 스케줄을 일시적으로 조정한다.

대각선 지지(Diagonal Support)에서는 사용 가능한 지지 형상이 여러 다리를 사용하는 걷기 입각보다 좁기 때문에 몸체 자세 제어(Body Orientation Control)가 특히 중요하다. 접촉력이 잘못 분배되면 롤과 피치 교란이 빠르게 증가할 수 있다. MPC는 각 발의 무게중심에 대한 모멘트 암을 고려하여 회전 운동에 미치는 영향을 예측한다. 이를 통해 최적화기는 병진 운동과 자세를 동시에 조절할 수 있는 차등 접촉력(Differential Contact Force)을 생성한다.

회전 트로트(Turning Trot)에서는 예측 제어기가 요 동역학(Yaw Dynamics)과 비대칭 착지점 움직임을 협응해야 한다. 목표 요 회전율은 미래의 몸체 자세를 변화시키며 발의 상대 위치에도 영향을 준다. 안쪽 다리와 바깥쪽 다리는 서로 다른 보폭을 필요로 할 수 있으며, 입각력은 마찰 제약조건을 위반하지 않으면서 필요한 요 모멘트를 생성해야 한다. 급격한 회전에서는 회전 운동과 병진 운동이 강하게 결합되어 있으므로 예측 모델링(Predictive Modeling)이 특히 유용하다.

지형 경사(Terrain Slope)는 힘 요구조건과 기준 형상을 모두 변화시킨다. 경사면에서는 중력의 일부가 지형 표면을 따라 작용하며, 목표 몸체 자세는 국부 지면 법선(Local Ground Normal)에 부분적으로 정렬될 수 있다. 등반이나 하강 과정에서는 마찰 여유(Friction Margin)가 특히 중요하다. 지형 인식형 MPC(Terrain-Aware MPC)는 추정된 표면 법선과 접촉 좌표계(Contact Frame)를 포함하여 실제 지지 표면과 일관된 방식으로 힘 제약조건을 표현할 수 있다.

거친 지형(Rough Terrain)은 발 높이와 접촉 타이밍이 명목 모델과 달라질 수 있기 때문에 추가적인 불확실성을 발생시킨다. 강건한 구현에서는 MPC를 적응형 착지점 계획(Adaptive Foothold Planning) 및 이벤트 기반 접촉 보정(Event-Based Contact Correction)과 결합한다. 다른 발이 지지를 확보하지 못하면 입각을 연장하거나 명령 속도를 낮추고 힘 여유를 증가시킬 수 있다. MPC는 예측적 협응을 제공하지만 환경 이벤트를 정확히 예측할 수 없는 경우에는 국부적인 반응형 메커니즘(Local Reactive Mechanism)이 여전히 필요하다.

외부 교란(External Disturbance)은 이동 예측 구간 제어의 장점을 잘 보여준다. 외력이 가해지면 추정된 몸체 속도와 각운동량이 즉시 변화한다. 다음 MPC 해는 사용 가능한 지면 반력을 재분배하고 미래의 대각선 접촉이 복구 과정에 어떻게 기여할 수 있는지를 예측한다. 힘 제어만으로 충분하지 않으면 착지점 계획기가 다음 유각 발의 위치를 변경하여 운동량 조절(Momentum Regulation)과 보정 발걸음(Corrective Stepping)을 결합할 수 있다.

솔버 성능(Solver Performance)은 실제 구현에서 핵심적인 고려사항이다. 최적화는 사용 가능한 제어 시간 간격 안에서 완료되어야 하며, 간헐적으로 발생하는 긴 계산 시간은 약간 덜 최적이더라도 계산 시간이 일정한 해보다 더 큰 문제가 될 수 있다. 이전 해를 이용한 웜 스타트(Warm Start), 희소 행렬(Sparse Matrix)의 활용, 모델 항의 사전 계산(Precomputation), 효율적인 이차 계획 솔버를 통해 지연 시간을 줄일 수 있다. 따라서 제어기 설계에서는 계산 아키텍처(Computational Architecture) 자체를 이동 성능의 일부로 고려해야 한다.

모델 불일치(Model Mismatch) 역시 관리해야 한다. 단일 강체 모델은 다리 관성(Leg Inertia), 관절 탄성(Joint Elasticity), 구동계 동역학(Drivetrain Dynamics), 충격 과도현상(Impact Transient), 일부 몸체 변형을 무시한다. 이러한 근사는 지면 반력을 계획하는 데에는 충분한 경우가 많지만 매우 빠르거나 고동적인 움직임에서는 정확도가 감소한다. 피드백 제어, 외란 추정(Disturbance Estimation), 모델 적응(Model Adaptation), 또는 학습 기반 잔차 모델(Learned Residual Model)을 이용하여 예측과 실제 하드웨어 거동 사이의 체계적인 차이를 보상할 수 있다.

안전 제약조건(Safety Constraint)은 명목 추종 목표와 독립적으로 항상 활성화되어야 한다. 관절 위치, 속도, 토크, 발 작업 공간(Foot Workspace), 마찰, 몸체 자세, 접촉력 한계를 실행 과정에서 감시할 수 있다. 최적화 문제가 실행 불가능(Infeasible)해지거나 상태 추정의 신뢰성이 낮아지는 경우 시스템은 제어되지 않은 명령을 적용하는 대신 보수적인 행동(Conservative Behavior)으로 전환해야 한다. 신뢰성 높은 이동을 위해서는 계산 또는 센싱 성능이 저하된 상황을 명시적으로 처리해야 한다.

따라서 MPC 기반 트로트 제어기(MPC-Based Trot Controller)는 하나의 최적화 루틴이 아니라 계층화된 폐루프 시스템(Layered Closed-Loop System)으로 이해하는 것이 적절하다. 보행 생성은 미래 접촉을 제공하고, 인식(Perception)과 상태 추정은 현재의 물리적 상태를 설명하며, MPC는 몸체 동역학을 예측하고 입각력을 최적화한다. 착지점 계획은 미래 지지를 구성하고 전신 제어는 이러한 결정을 관절 구동을 통해 실현한다. 피드백은 수학적 예측과 실제 로봇을 지속적으로 다시 연결한다.

피지컬 AI(Physical AI)의 관점에서 이러한 아키텍처는 예측(Prediction)이 어떻게 물리적 행동(Physical Action)으로 변환되는지를 보여준다. 로봇은 후보 접촉력이 적용될 때 몸체가 어떻게 변화할지를 예측하고, 이동 목표와 물리적 제약조건을 만족하는 행동을 선택하며, 다리를 통해 해당 행동을 실행한 후 결과 상태를 다시 관측한다. 이러한 과정을 높은 주파수로 반복함으로써 속도, 지형, 접촉 조건, 외부 교란이 지속적으로 변화하는 상황에서도 안정적인 트로트(Trot)를 유지할 수 있다.

## 03.07. Stair Climbing Gait Adaptation [w/Code]

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

계단 등반(Stair Climbing)은 4족 로봇(Quadruped)이 일반적인 이동 방식을 구조화되어 있지만 강한 불연속성을 갖는 3차원 지형에 적응하도록 요구한다. 평지 보행(Flat-Ground Walking)과 달리 각각의 계단은 수직 장애물, 제한된 지지 표면, 반복적인 몸체 높이 변화를 발생시킨다. 따라서 성공적인 이동을 위해서는 보행 타이밍(Gait Timing), 착지점 배치(Foothold Placement), 유각 발 여유 높이(Swing-Foot Clearance), 몸체 자세(Body Posture), 접촉력(Contact Force), 안정성 여유(Stability Margin)를 협응하여 적응시켜야 한다.

첫 번째 요구조건은 계단 형상(Stair Geometry)을 신뢰성 있게 인식하는 것이다. 로봇은 디딤면 깊이(Tread Depth), 계단 높이(Riser Height), 계단 경사(Staircase Inclination), 모서리 위치(Edge Location), 그리고 몸체에 대한 계단의 방향을 추정해야 한다. 깊이 카메라(Depth Camera), 라이다(LiDAR), 스테레오 비전(Stereo Vision) 또는 기타 거리 센서를 이용하여 포인트 클라우드(Point Cloud)와 고도 지도(Elevation Map)를 생성하고, 이로부터 반복되는 평면과 수직 불연속면을 추출할 수 있다. 작은 착지점 오차만으로도 발이 계단 모서리 근처에 놓일 수 있으므로 정확한 형상 정보가 필수적이다.

계단 인식(Stair Perception)은 사용 가능한 디딤면(Tread Surface)을 수직면(Riser) 및 불확실한 영역과 구분해야 한다. 기하학적으로 평평한 영역이라도 폭이 지나치게 좁거나 모서리에 너무 가까우면 자동으로 안전한 착지점이 되는 것은 아니다. 인식 시스템은 표면 방향, 사용 가능한 접촉 면적, 모서리까지의 거리, 측정 신뢰도(Measurement Confidence), 추정 마찰(Estimated Friction)에 따라 주행 가능성(Traversability) 또는 착지점 품질(Foothold Quality)을 부여할 수 있다. 이러한 값은 착지점 계획기(Foothold Planner)의 제약조건이나 비용으로 사용된다.

로봇은 등반을 시작하기 전에 접근 정렬(Approach Alignment)도 결정해야 한다. 큰 요 정렬 오차(Yaw Misalignment)가 존재하면 왼쪽과 오른쪽 다리가 계단 모서리를 서로 다른 종방향 위치에서 만나게 되어 발 배치가 복잡해지고 충돌 위험이 증가한다. 내비게이션 또는 국부 계획 계층(Local Planning Layer)은 상승을 시작하기 전에 몸체를 계단 방향으로 회전시킬 수 있다. 이후 남아 있는 작은 정렬 오차는 비대칭 착지점(Asymmetric Foothold)과 몸체 요 제어(Body-Yaw Control)를 통해 보상할 수 있다.

보수적인 계단 등반 보행(Conservative Stair-Climbing Gait)은 일반적으로 동적인 평지 이동보다 듀티 팩터(Duty Factor)와 접촉 중첩(Contact Overlap)을 증가시킨다. 보행 주기의 상당 부분에서 세 개 또는 최소 두 개의 신뢰할 수 있는 지지 접촉을 유지하면 신중한 발 배치와 하중 전달을 수행할 시간을 확보할 수 있다. 따라서 불확실한 계단에서는 걷기형 패턴(Walking-Type Pattern)이 일반적으로 적합하지만, 계단 형상이 규칙적이고 정확하게 알려진 경우에는 보다 동적인 로봇이 트로트형 패턴(Trot-Like Pattern)을 사용하여 등반할 수도 있다.

착지점 계획(Foothold Planning)은 각각의 발이 수직면이나 모서리 근처가 아니라 디딤면에 착지해야 하기 때문에 매우 구조화된다. 목표 속도로부터 예측된 명목 착지점(Nominal Foothold)은 목표 계단의 안전 영역으로 투영되거나 최적화된다. 디딤면의 앞쪽과 뒤쪽 모서리 모두에서 안전 여유(Safety Margin)를 유지해야 한다. 선택된 지점은 동시에 다리 도달 가능성(Leg Reachability), 충돌 제약조건(Collision Constraint), 미래 지지 요구조건(Future Support Requirement)을 만족해야 한다.

계획기는 각 다리가 어느 계단 높이(Stair Level)를 목표로 해야 하는지도 결정해야 한다. 몸체 길이, 디딤면 깊이, 다리 작업 공간(Leg Workspace)에 따라 앞다리와 뒷다리가 동시에 서로 다른 높이의 계단을 점유할 수 있다. 이로 인해 발들이 서로 다른 높이에 위치하는 3차원 지지 구성(Three-Dimensional Support Configuration)이 형성된다. 따라서 제어기는 모든 입각 발이 하나의 공통 지면 평면에 있다고 가정하는 대신 전체 공간 좌표(Spatial Coordinate)에서 접촉 위치를 고려해야 한다.

유각 발 궤적(Swing-Foot Trajectory)은 평지보다 훨씬 큰 수직 여유 높이를 필요로 한다. 상승 과정에서 발은 상부 디딤면으로 이동하기 전에 계단 수직면을 넘어야 한다. 단순한 평지용 원호 궤적(Flat-Ground Arc)은 최종 착지점이 유효하더라도 수직면과 충돌할 수 있다. 따라서 궤적은 장애물 형상을 명시적으로 고려해야 하며, 유각 과정 전체에서 발과 하부 다리 모두에 충분한 여유 공간을 제공해야 한다.

계단 인식형 유각 궤적(Stair-Aware Swing Trajectory)은 움직임을 상승, 전진, 하강 요소로 구분할 수 있다. 발을 먼저 예상되는 계단 모서리보다 위로 들어 올린 후 디딤면 위쪽으로 전진시키고, 마지막으로 선택된 접촉 지점을 향해 하강시킬 수 있다. 부드러운 다항식(Polynomial), 스플라인(Spline), 베지어 곡선(Bézier Curve)을 이용하여 연속적인 속도와 가속도를 유지하면서 이러한 구간을 연결할 수 있다. 여유 높이에는 인식 불확실성(Perception Uncertainty)과 추종 오차(Tracking Error)를 고려한 안전 여유가 포함되어야 한다.

충돌 회피(Collision Avoidance)는 다리 전체의 형상을 고려해야 한다. 발이 계단 모서리를 통과하더라도 정강이(Shin)나 무릎(Knee)이 수직면과 충돌할 수 있으며, 특히 높은 계단을 오를 때 이러한 위험이 증가한다. 계획기는 무릎 굽힘(Knee Flexion)을 증가시키거나 고관절 움직임(Hip Motion)을 수정하고, 몸체를 높이거나 수평 이동 경로를 변경해야 할 수 있다. 따라서 단순히 종단점(Endpoint)만 확인하는 것보다 전체 유각 궤적에 걸쳐 운동학적 검사(Kinematic Check)를 수행하는 것이 중요하다.

몸체 높이 적응(Body-Height Adaptation)은 계단을 오르는 동안 다리의 도달 가능성을 향상시킨다. 발이 서로 다른 높이의 계단을 점유하는 상황에서 몸체를 고정된 세계 좌표 높이(World Height)에 유지하면 앞다리나 뒷다리가 극단적인 관절 구성에 도달할 수 있다. 제어기는 유용한 관절 여유(Joint Margin)를 유지하면서 상승 과정에 따라 무게중심(Center of Mass)을 점진적으로 높일 수 있다. 목표 몸체 높이는 하나의 수평 지면이 아니라 국부적인 계단 프로파일(Local Staircase Profile)을 기준으로 설정할 수 있다.

몸체 피치(Body Pitch) 역시 중요한 변수이다. 계단 경사에 맞춘 적절한 피치는 작업 공간 분배(Workspace Distribution)를 개선하고 극단적인 다리 신장을 줄일 수 있지만, 지나친 피치는 안정성을 저하시키거나 센서 가시성(Sensor Visibility)을 감소시킬 수 있다. 선호되는 자세는 로봇의 형태(Morphology)와 계단 형상에 따라 달라진다. 전신 제어(Whole-Body Control)는 피치를 조절하면서 도달 가능성과 접촉력 분배를 향상시키는 제한적인 자세 적응을 허용할 수 있다.

계단 상승은 로봇이 지속적으로 중력 위치 에너지(Gravitational Potential Energy)를 증가시켜야 하므로 필요한 지면 반력(Ground Reaction Force)을 변화시킨다. 입각 다리는 수직 지지와 함께 전진 추진력 및 몸체 모멘트 조절을 제공해야 한다. 하중은 각 발의 위치, 마찰 능력(Friction Capability), 관절 토크 여유(Joint Torque Margin)에 따라 분배되어야 한다. 새롭게 상단 계단에 놓인 발로 하중을 갑작스럽게 전달하면 미끄러짐이나 과도한 충격이 발생할 수 있다.

따라서 착지 이후의 제어된 하중 전달(Controlled Load Transfer)이 필수적이다. 유각 발이 상부 디딤면에 도달하면 상당한 지지력을 부여하기 전에 접촉을 확인해야 한다. 제어기는 다른 다리의 하중을 감소시키면서 새롭게 접촉한 발의 법선력(Normal Force)을 점진적으로 증가시킬 수 있다. 힘 센서(Force Sensor), 관절 토크 추정(Joint Torque Estimation), 또는 고유수용성 접촉 감지(Proprioceptive Contact Detection)를 이용하면 다음 다리가 유각을 시작하기 전에 새로운 착지점이 물리적으로 신뢰할 수 있는지를 판단할 수 있다.

모델 예측 제어(Model Predictive Control)는 미래 예측 구간에 걸쳐 변화하는 이러한 지지 조건을 협응할 수 있다. 접촉 스케줄(Contact Schedule)은 각 발이 어느 계단 높이를 점유할 것으로 예상되는지를 나타내며, 예측 모델(Predictive Model)은 미래의 몸체 움직임과 필요한 지면 반력을 추정한다. MPC는 몸체 높이와 지지 형상의 변화가 실제로 발생하기 전에 이를 준비할 수 있으므로 순수한 반응형 힘 제어(Reactive Force Control)에 비해 안정성을 향상시킬 수 있다.

계단 등반에서는 발걸음 주파수(Step Frequency)와 보폭 길이(Stride Length)를 조정해야 할 수 있다. 높은 주파수는 정확한 유각 발 배치와 접촉 확인에 사용할 수 있는 시간을 감소시키며, 지나치게 긴 보폭은 로봇이 안전한 디딤면 영역을 건너뛰거나 다리 작업 공간을 초과하도록 만들 수 있다. 신중한 제어기는 일반적으로 전진 속도를 낮추고 사용 가능한 유각 및 입각 시간을 증가시킨다. 계단 형상과 접촉 신뢰성이 충분히 확보된 규칙적인 계단에서는 보다 빠른 이동이 가능하다.

접촉 타이밍(Contact Timing)은 순수한 주기적 방식보다 이벤트 인식형(Event-Aware)으로 유지되어야 한다. 지형 인식 오차로 인해 발이 예상보다 일찍 계단 모서리와 접촉하거나 예상된 높이에서 디딤면을 찾지 못할 수 있다. 조기 접촉(Early Contact)이 발생하면 수직면을 강하게 밀지 않도록 유각 명령을 신속하게 수정해야 한다. 지연 접촉(Late Contact)이 발생하면 다른 다리들이 계속 몸체를 지지하는 동안 제어된 하향 탐색(Controlled Downward Search)이 필요할 수 있다.

예상하지 못한 접촉은 지형 모델(Terrain Model)을 개선하는 데에도 사용할 수 있다. 발이 예측된 높이보다 위쪽 또는 아래쪽의 표면과 접촉한다면 이러한 차이는 계단 형상에 대한 직접적인 물리적 증거(Physical Evidence)를 제공한다. 피지컬 AI(Physical AI) 시스템은 이러한 접촉 정보를 비전 또는 거리 기반 인식과 융합하여 국부 고도 추정(Local Elevation Estimate)을 갱신할 수 있다. 이 경우 이동은 발걸음이 움직임을 실행하는 동시에 환경 구조를 검증하는 능동 센싱(Active Sensing) 과정이 된다.

계단 하강(Stair Descent)은 상승과는 다른 동역학적 문제를 가진다. 로봇은 중력 가속도를 제어하고 큰 착지 충격을 방지하면서 무게중심을 낮춰야 한다. 유각 발은 계단 모서리에 의해 부분적으로 가려질 수 있는 낮은 표면을 향해 이동한다. 따라서 인식 불확실성이 더 커지는 경우가 많으며, 제어기는 나머지 입각 다리를 통해 강한 지지를 유지하면서 제어된 수직 속도로 착지에 접근해야 한다.

하강 과정에서 과도한 전방 몸체 움직임은 무게중심이 복구 가능한 지지 구성(Recoverable Support Configuration)을 벗어나도록 만들 수 있다. 따라서 착지점과 몸체 속도를 함께 계획해야 한다. 앞다리가 낮은 계단에 접촉하는 동안 뒷다리는 높은 계단에서 하강을 조절할 수 있다. 제동력(Braking Force)과 몸체 피치 제어는 특히 가파른 계단이나 낮은 마찰 표면에서 제어되지 않은 전방 회전을 방지하는 데 도움을 준다.

마찰(Friction)은 상승과 하강 모두에서 매우 중요하다. 제한된 디딤면은 힘을 적용할 수 있는 위치를 제한하며, 큰 접선력(Tangential Force)은 발이 계단 모서리 방향으로 미끄러지게 만들 수 있다. 힘 최적화(Force Optimization)는 추정된 마찰 한계에서 직접 동작하기보다 적절한 마찰 여유(Friction Margin)를 유지해야 한다. 표면이 젖어 있거나 매끄럽거나 먼지가 많거나 기타 불확실성이 존재하는 것으로 판단되면 로봇은 속도를 낮추고 접촉 중첩을 증가시킬 수 있다.

안정성 평가(Stability Assessment)는 실제 3차원 지지 형상을 고려해야 한다. 기존의 평면 지지 다각형(Planar Support Polygon)은 유용한 직관을 제공하지만 발들이 서로 다른 높이에 있고 동적 효과가 중요한 경우에는 충분하지 않다. 중심 운동량(Centroidal Momentum), 예측 접촉 실현 가능성(Predicted Contact Feasibility), 힘 한계(Force Limit), 도달 가능한 보정 착지점(Reachable Corrective Foothold)은 보다 일반적인 안정성 척도를 제공한다. 남아 있는 접촉만으로 다음 움직임을 안전하게 지지할 수 없다면 제어기는 다리를 들어 올리는 동작을 지연해야 한다.

계단 위에서의 회전(Turning on Stairs)은 착지 가능한 영역이 좁고 불연속적인 높이에 위치하기 때문에 복잡성을 더욱 증가시킨다. 큰 요 변화는 발을 계단 모서리에 가깝게 만들거나 다리 교차(Leg Crossing)를 발생시킬 수 있다. 가능하면 주요 방향 전환은 계단참(Landing)이나 충분히 넓은 디딤면에서 수행하는 것이 바람직하다. 등반 중 회전이 불가피한 경우 계획기는 작은 단위의 요 변화를 사용하고 각 다리의 도달 가능한 안전 영역을 독립적으로 평가해야 한다.

로봇 형태(Robot Morphology)는 통과할 수 있는 계단 형상을 결정한다. 최대 계단 높이는 다리 길이, 관절 가동 범위(Joint Range), 몸체 여유 높이(Body Clearance), 토크 성능(Torque Capability), 충돌 형상(Collision Geometry)에 따라 결정된다. 디딤면 깊이는 신뢰할 수 있는 접촉을 위한 충분한 면적을 제공하고 여러 다리가 실현 가능한 구성을 유지할 수 있어야 한다. 따라서 계단 등반 제어기는 감지된 모든 계단이 통과 가능하다고 가정하는 대신 명시적인 로봇 성능 한계(Robot Capability Limit)를 기준으로 지형을 평가해야 한다.

학습 기반 제어(Learning-Based Control)는 모델 기반 계단 적응(Model-Based Stair Adaptation)을 보완할 수 있다. 강화학습(Reinforcement Learning)은 시뮬레이션에서 로봇이 다양한 계단 높이, 디딤면 깊이, 마찰, 센싱 잡음(Sensing Noise), 외란(Disturbance)을 경험하도록 할 수 있다. 학습된 정책(Learned Policy)은 수작업으로 설계하기 어려운 유용한 협응 전략을 개발할 수 있다. 그러나 학습된 행동을 실제 하드웨어로 전이하기 위해서는 명시적인 인식, 도달 가능성 검사, 접촉 제약조건, 안전 한계가 여전히 중요하다.

고장 복구(Failure Recovery)는 처음부터 계단 이동 시스템에 포함되어야 한다. 발이 미끄러지거나 디딤면을 놓치거나 예상하지 못한 장애물과 접촉하면 로봇은 명목 보행을 즉시 계속하지 않아야 한다. 선택된 접촉을 고정하고 몸체를 낮추며 가능한 경우 지지 영역을 넓히거나 문제가 발생한 발을 보다 안전한 위치로 되돌릴 수 있다. 복구 행동(Recovery Behavior)은 상승 또는 하강을 다시 시작하기 전에 신뢰할 수 있는 지지를 복원하는 것을 우선해야 한다.

따라서 계단 등반 보행 적응(Stair-Climbing Gait Adaptation)은 인식(Perception), 보행 타이밍, 3차원 착지점 계획(Three-Dimensional Foothold Planning), 충돌 인식형 유각 운동(Collision-Aware Swing Motion), 예측 힘 제어(Predictive Force Control), 이벤트 기반 피드백(Event-Based Feedback)을 통합한다. 로봇은 계단에 대한 기하학적 모델과 실제 접촉 관측을 지속적으로 일치시켜야 한다. 각 계단에 맞추어 몸체 자세, 지지 타이밍, 착지점, 힘을 조절함으로써 4족 로봇은 명목 보행을 지형 특화 이동 전략(Terrain-Specific Locomotion Strategy)으로 변환할 수 있다.

피지컬 AI(Physical AI)의 관점에서 계단은 이동 문제를 인식과 제어라는 독립적인 문제로 분리할 수 없는 이유를 잘 보여준다. 로봇은 구조화된 형상을 관측하고, 실현 가능한 접촉을 예측하며, 선택된 지지 표면을 향해 다리를 이동시키고, 착지를 통해 그 예측을 물리적으로 검증한 다음 그 결과를 이용하여 미래 행동을 갱신한다. 신뢰성 높은 계단 등반은 환경 이해(Environmental Understanding), 예측(Prediction), 행동(Action), 접촉(Contact) 사이에서 반복적으로 수행되는 이러한 폐루프(Closed Loop)를 통해 구현된다.

## 03.08. Dynamic Gait Pronk Gallop at High Speed [w/Code]

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

고속 동적 보행(High-Speed Dynamic Gait)은 4족 로봇(Quadruped)이 짧은 접촉 시간(Contact Time), 큰 지면 반력(Ground Reaction Force), 빠른 다리 움직임(Leg Motion), 그리고 빈번한 공중 구간(Aerial Phase)을 이용하여 높은 이동 속도를 달성하는 보행 형태이다. 프롱크(Pronk)와 갤럽(Gallop)은 대표적인 동적 보행(Dynamic Gait)으로, 일반적인 걷기(Walk)나 트로트(Trot)보다 운동량(Momentum), 탄성 에너지(Elastic Energy), 접촉 타이밍(Contact Timing)을 적극적으로 활용한다. 이러한 보행에서는 정적 안정성(Static Stability)보다 주기적인 동역학적 안정성(Dynamic Stability)과 정확한 상태 예측(State Prediction)이 훨씬 중요하다.

프롱크(Pronk)는 네 다리가 거의 동시에 입각(Stance)과 유각(Swing)을 수행하는 대칭적인 보행 패턴(Symmetric Gait Pattern)이다. 모든 발이 비슷한 시점에 지면을 밀어 몸체를 공중으로 추진하고, 공중 구간 이후 다시 거의 동시에 착지(Touchdown)한다. 이러한 동기화된 접촉 구조(Synchronized Contact Structure)는 보행 패턴 자체는 비교적 단순하게 만들지만, 짧은 입각 구간 동안 전체 몸체 운동량(Whole-Body Momentum)을 조절해야 하므로 높은 순간 힘(Peak Force)과 정밀한 착지 제어(Touchdown Control)가 요구된다.

프롱크의 한 주기는 일반적으로 압축(Compression), 추진(Propulsion), 비행(Flight), 착지(Landing) 과정으로 해석할 수 있다. 착지 직후 다리는 몸체의 하강 운동을 흡수하면서 압축되고, 이후 지면을 밀어 다음 비행 구간에 필요한 수직 및 전방 운동량을 생성한다. 공중에서는 외부 접촉력(External Contact Force)이 거의 존재하지 않으므로 몸체의 궤적(Body Trajectory)은 이륙(Liftoff) 순간에 형성된 속도와 각운동량(Angular Momentum)에 크게 의존한다.

갤럽(Gallop)은 프롱크보다 복잡한 비대칭 동적 보행(Asymmetric Dynamic Gait)으로, 앞다리와 뒷다리 사이에 명확한 위상 차이(Phase Difference)를 갖는다. 일반적으로 뒷다리가 강한 추진력을 생성하고 앞다리가 착지와 몸체 자세 조절(Body Attitude Regulation)에 중요한 역할을 수행한다. 다리 접촉은 동시에 발생하기보다 일정한 순서로 진행되며, 이러한 순차적인 접촉(Sequential Contact)을 통해 높은 전진 속도와 긴 보폭(Stride Length)을 형성할 수 있다.

갤럽은 몸체의 피치 운동(Pitch Motion)을 적극적으로 이용한다. 뒷다리가 지면을 밀 때 몸체는 전방으로 추진되며 특정 피치 운동량(Pitch Momentum)을 얻게 되고, 앞다리 착지는 이를 흡수하거나 다음 주기를 위해 재조정한다. 따라서 갤럽 제어에서는 단순한 무게중심 위치(Center-of-Mass Position)뿐만 아니라 몸체 각속도(Angular Velocity)와 각운동량을 함께 관리해야 한다. 몸체 피치와 다리 접촉 순서가 잘못 결합되면 착지 충격(Landing Impact)이나 전방 회전 불안정성(Forward Rotational Instability)이 빠르게 증가할 수 있다.

고속 보행에서는 듀티 팩터(Duty Factor)가 감소하는 경향이 있으며, 각 다리가 지면과 접촉하는 시간이 짧아진다. 짧은 입각 시간 동안 필요한 운동량 변화를 만들어야 하므로 평균 및 최대 지면 반력이 증가할 수 있다. 동시에 공중 구간이 길어지면서 지면을 이용한 상태 보정(State Correction) 기회는 감소한다. 따라서 제어기는 각 접촉을 단순한 지지 이벤트(Support Event)가 아니라 다음 비행 상태를 결정하는 운동량 조절 구간(Momentum Regulation Phase)으로 취급해야 한다.

보행 주파수(Gait Frequency)와 보폭(Stride Length)은 고속 이동 성능을 결정하는 핵심 변수이다. 이동 속도는 일반적으로 발걸음 주파수(Step Frequency)와 유효 보폭(Effective Stride Length)의 조합으로 형성되지만, 두 값을 무제한으로 증가시킬 수는 없다. 높은 주파수는 액추에이터 속도(Actuator Speed)와 다리 관성(Leg Inertia)의 영향을 증가시키고, 긴 보폭은 관절 작업 공간(Joint Workspace)과 착지 안정성(Landing Stability)을 제한한다. 따라서 목표 속도에 따라 주파수와 보폭 사이의 적절한 균형을 찾아야 한다.

고속 프롱크와 갤럽에서는 상태 추정 지연(State-Estimation Delay)이 특히 중요한 문제가 된다. 저속에서는 수십 밀리초의 오차가 비교적 작은 위치 차이로 나타날 수 있지만, 고속에서는 동일한 지연이 상당한 몸체 및 발 위치 오차로 변환된다. 관성 측정 장치(Inertial Measurement Unit), 관절 엔코더(Joint Encoder), 접촉 정보(Contact Information), 외부 위치 추정(External Pose Estimation) 정보를 빠르게 융합하여 현재 상태를 추정해야 하며, 제어 지연(Control Delay)을 보상하기 위한 미래 상태 예측(Future-State Prediction)도 필요하다.

접촉 감지(Contact Detection)는 동적 보행의 위상 동기화(Phase Synchronization)에 직접적으로 사용된다. 계획된 착지 시간과 실제 접촉 시간 사이에는 지형 높이, 몸체 상태, 모델 오차(Model Error)로 인해 차이가 발생할 수 있다. 실제 착지가 예상보다 빠르거나 늦으면 고정된 시간 기반 보행 패턴(Time-Based Gait Pattern)은 다음 접촉까지 연속적인 오차를 누적할 수 있다. 이벤트 기반 위상 보정(Event-Based Phase Correction)은 실제 접촉을 이용하여 보행 오실레이터(Gait Oscillator)나 접촉 스케줄(Contact Schedule)을 다시 동기화할 수 있다.

고속 착지에서는 충격 관리(Impact Management)가 핵심적인 설계 요소이다. 큰 하향 속도를 가진 발과 몸체가 지면과 접촉하면 매우 짧은 시간에 큰 충격력이 발생할 수 있다. 다리 순응성(Leg Compliance), 관절 임피던스(Joint Impedance), 목표 착지 속도(Desired Touchdown Velocity), 액추에이터 토크 제어(Actuator Torque Control)를 이용하여 충격을 흡수해야 한다. 지나치게 강한 제어는 충격을 구조물에 전달할 수 있으며, 지나치게 부드러운 제어는 자세 붕괴(Posture Collapse)나 과도한 다리 압축을 유발할 수 있다.

탄성 에너지(Elastic Energy)의 저장과 반환은 효율적인 동적 보행에서 중요한 역할을 한다. 실제 동물과 유사하게 로봇의 다리 또는 구동계(Drivetrain)가 적절한 순응성을 가지면 착지 시 발생하는 에너지 일부를 저장하고 추진 과정에서 다시 사용할 수 있다. 직렬 탄성 액추에이터(Series Elastic Actuator)나 기계적 탄성 요소(Mechanical Elastic Element)뿐만 아니라 능동 임피던스 제어(Active Impedance Control)를 통해 가상적인 스프링-댐퍼(Virtual Spring-Damper) 특성을 구현할 수도 있다.

프롱크 제어에서는 네 다리의 힘 대칭성(Force Symmetry)이 몸체 자세 유지에 중요하다. 한쪽 다리가 다른 다리보다 더 큰 힘을 발생시키거나 접촉 시간이 달라지면 원하지 않는 롤(Roll), 피치(Pitch), 또는 요(Yaw) 모멘트가 생성될 수 있다. 따라서 각 발의 힘을 동일하게 만드는 것만으로 충분하지 않으며, 실제 접촉 위치(Contact Position)와 무게중심에 대한 모멘트 암(Moment Arm)을 고려하여 전체 힘과 모멘트를 원하는 값으로 만들어야 한다.

갤럽에서는 힘 분배(Force Distribution)가 본질적으로 비대칭적이고 시간에 따라 빠르게 변화한다. 뒷다리는 추진 단계(Propulsion Phase)에서 큰 전방 및 수직 힘을 생성할 수 있으며, 앞다리는 착지 이후 감속(Deceleration)과 자세 안정화(Attitude Stabilization)에 더 크게 기여할 수 있다. 제어기는 이러한 역할 차이를 허용하면서도 전체 주기에서 목표 선운동량(Linear Momentum)과 각운동량이 유지되도록 접촉력을 계획해야 한다.

모델 예측 제어(Model Predictive Control)는 고속 동적 보행을 다루는 유용한 방법이다. 예측 구간(Prediction Horizon)에 미래 입각 상태와 공중 상태를 포함하면 제어기는 현재 접촉력이 다음 비행 궤적(Flight Trajectory)과 착지 상태(Landing State)에 미치는 영향을 미리 평가할 수 있다. 특히 갤럽과 같이 접촉 순서가 복잡한 보행에서는 미래의 다리 접촉을 고려한 운동량 계획(Momentum Planning)이 단순한 순간 피드백(Instantaneous Feedback)보다 효과적인 제어를 제공할 수 있다.

공중 구간에서는 발을 통한 지면 반력을 사용할 수 없기 때문에 몸체의 병진 운동(Translational Motion)을 직접 변경할 수 없다. 그러나 다리의 움직임을 이용하여 몸체의 관성 분포(Inertia Distribution)와 각운동량 관계를 조절할 수 있다. 빠른 다리 스윙(Leg Swing)은 몸체 자세에 반작용(Reaction)을 발생시킬 수 있으며, 이를 이용하여 착지 전에 피치나 롤 상태를 제한적으로 조절할 수 있다. 이러한 효과는 고속 보행에서 무시하기 어려워진다.

착지점 계획(Foothold Planning)은 속도가 증가할수록 더욱 예측적이어야 한다. 발이 유각을 시작한 순간의 몸체 위치만을 기준으로 목표점을 결정하면 착지 시점에는 몸체가 이미 상당한 거리를 이동해 있을 수 있다. 따라서 예상 착지 시간의 몸체 위치와 속도, 회전 상태(Rotational State)를 예측하여 착지점을 결정해야 한다. 보정 착지점(Corrective Foothold)은 다음 입각에서 필요한 제동이나 추진 효과까지 고려할 수 있다.

유각 발 궤적(Swing-Foot Trajectory)은 빠르면서도 충돌에 안전해야 한다. 고속 이동에서는 유각 시간이 짧아 높은 관절 속도와 가속도가 필요하지만, 발을 지나치게 높이 들어 올리면 에너지 소비(Energy Consumption)와 관성 부하(Inertial Load)가 증가한다. 반대로 여유 높이(Clearance)가 부족하면 작은 지형 변화에도 발이 장애물과 충돌할 수 있다. 따라서 속도와 지형 불확실성(Terrain Uncertainty)에 따라 최소한의 안전 여유를 동적으로 조절하는 것이 중요하다.

액추에이터 성능(Actuator Performance)은 가능한 최고 보행 속도를 직접 제한한다. 모터의 최대 토크뿐만 아니라 최대 속도, 토크-속도 특성(Torque-Speed Characteristic), 순간 출력(Peak Power), 열 한계(Thermal Limit), 감속기 효율(Gearbox Efficiency)이 모두 중요하다. 고속 보행에서는 짧은 시간 동안 큰 기계적 출력(Mechanical Power)을 반복적으로 요구하므로 정적인 최대 토크만으로 성능을 평가해서는 안 된다. 지속 출력(Continuous Power)과 피크 출력(Peak Power)의 차이도 반드시 고려해야 한다.

다리 관성(Leg Inertia)은 고속에서 중요한 에너지 및 제어 요소가 된다. 무거운 말단 링크(Distal Link)를 빠르게 앞뒤로 움직이면 상당한 관성 토크(Inertial Torque)와 에너지 소비가 발생한다. 따라서 동적 4족 로봇은 일반적으로 무거운 액추에이터를 몸체 가까이에 배치하고 원위부 다리 질량(Distal Leg Mass)을 줄이는 설계를 선호한다. 낮은 다리 관성은 높은 보행 주파수를 가능하게 하고 접촉 직전의 발 위치 수정 능력도 향상시킨다.

마찰 제약(Friction Constraint)은 고속 추진과 제동 모두에서 중요하다. 강한 전방 추진력을 얻기 위해 접선 지면 반력(Tangential Ground Reaction Force)을 증가시키면 발이 마찰 한계(Friction Limit)에 가까워질 수 있다. 미끄러짐(Slip)이 발생하면 계획된 운동량 변화가 만들어지지 않을 뿐만 아니라 몸체 자세도 빠르게 무너질 수 있다. 제어기는 추정 마찰계수(Estimated Friction Coefficient)보다 충분한 여유를 유지하면서 가능한 접촉력을 계산해야 한다.

고속 회전(High-Speed Turning)에서는 선형 운동과 요 운동(Yaw Motion)이 강하게 결합된다. 좌우 다리의 착지 위치, 접촉 시간, 추진력이 달라져야 원하는 회전 반경(Turning Radius)을 만들 수 있다. 지나치게 큰 요 명령은 바깥쪽 다리의 마찰 한계를 초과하거나 안쪽 다리를 불리한 작업 공간으로 밀어 넣을 수 있다. 따라서 속도가 증가할수록 허용 가능한 회전율(Yaw Rate)과 곡률(Curvature)을 제한하는 것이 필요하다.

지형 불확실성(Terrain Uncertainty)은 동적 보행의 사용 가능 범위를 제한한다. 평탄하고 예측 가능한 지면에서는 프롱크나 갤럽을 높은 속도로 실행할 수 있지만, 거친 지형(Rough Terrain)에서는 짧은 접촉 시간과 긴 공중 구간 때문에 복구 기회(Recovery Opportunity)가 크게 감소한다. 지형 인식(Terrain Perception) 결과에 따라 보행 속도, 듀티 팩터, 유각 높이 또는 보행 모드 자체를 변경하는 적응 전략(Adaptive Strategy)이 필요하다.

동적 보행으로의 전환(Gait Transition)도 점진적으로 이루어져야 한다. 트로트에서 갤럽으로 전환할 때는 단순히 접촉 순서를 변경하는 것이 아니라 몸체 운동량, 보폭, 주파수, 피치 진동(Pitch Oscillation)을 새로운 주기적 상태(Periodic State)로 이동시켜야 한다. 반대로 고속 갤럽에서 감속할 때는 운동에너지(Kinetic Energy)를 안전하게 소산하면서 접촉 중첩을 증가시키고 보다 안정적인 보행으로 전환해야 한다.

강화학습(Reinforcement Learning)은 프롱크와 갤럽 같은 복잡한 동적 보행을 생성하는 데 유용할 수 있다. 정책(Policy)은 목표 속도와 상태 정보를 입력받아 관절 목표(Joint Target), 토크(Torque), 또는 잔차 제어 명령(Residual Control Command)을 생성하도록 학습할 수 있다. 다양한 속도, 마찰, 지형, 질량, 지연 조건을 포함한 훈련을 통해 강건성(Robustness)을 향상시킬 수 있으며, 명시적으로 설계하기 어려운 자연스러운 동적 협응 패턴(Dynamic Coordination Pattern)을 발견할 가능성도 있다.

그러나 학습된 고속 정책(Learned High-Speed Policy)은 하드웨어 한계를 명시적으로 고려해야 한다. 시뮬레이션에서는 순간적으로 가능한 것처럼 보이는 토크나 관절 속도가 실제 모터, 감속기, 배터리, 구조물에서는 허용되지 않을 수 있다. 도메인 랜덤화(Domain Randomization), 액추에이터 모델링(Actuator Modeling), 지연 모델링(Delay Modeling), 토크 제한(Torque Limit), 열 제한(Thermal Limit)을 훈련 과정에 포함해야 하며 실제 로봇에서는 별도의 안전 계층(Safety Layer)을 유지해야 한다.

고속 동적 보행의 실패 복구(Failure Recovery)는 일반적인 저속 보행보다 어렵다. 접촉 하나가 실패했을 때 몸체가 이미 큰 운동량을 가지고 있기 때문에 다음 정상 보행 주기까지 기다릴 시간이 부족할 수 있다. 제어기는 즉각적인 보정 착지(Corrective Touchdown), 비상 접촉 연장(Emergency Contact Extension), 몸체 자세 변경, 또는 안전한 낙상 동작(Safe-Fall Behavior)을 선택해야 할 수 있다. 따라서 복구 가능 영역(Recoverable Region)을 사전에 예측하는 것이 중요하다.

프롱크와 갤럽의 성능은 단순한 최고 속도만으로 평가해서는 안 된다. 속도 추종 오차(Velocity Tracking Error), 자세 안정성(Attitude Stability), 착지 충격, 미끄러짐 빈도(Slip Frequency), 에너지 소비, 액추에이터 열 부하(Thermal Load), 최대 접촉력(Peak Contact Force), 복구 성능(Recovery Performance)을 함께 평가해야 한다. 동일한 속도를 달성하더라도 더 낮은 충격과 에너지로 반복 가능한 보행을 수행하는 제어기가 실제 시스템에서는 더 우수할 수 있다.

피지컬 AI(Physical AI) 관점에서 고속 동적 보행은 예측(Prediction)과 물리적 상호작용(Physical Interaction)의 결합이 극단적으로 나타나는 사례이다. 로봇은 미래 접촉이 발생하기 전에 자신의 운동량과 착지 상태를 예측하고, 짧은 지면 접촉을 이용하여 다음 공중 상태를 형성해야 한다. 이후 실제 착지 결과를 다시 관측하여 다음 행동을 수정한다. 이러한 빠른 폐루프(Fast Closed Loop)는 고속 이동을 단순한 궤적 추종(Trajectory Tracking)이 아니라 지속적인 물리적 예측과 검증(Physical Prediction and Validation) 과정으로 만든다.

따라서 고속 프롱크와 갤럽 제어(High-Speed Pronk and Gallop Control)는 보행 위상(Gait Phase), 운동량 계획(Momentum Planning), 접촉력, 착지점, 몸체 자세, 액추에이터 성능, 지형 조건을 하나의 통합된 동적 시스템(Integrated Dynamic System)으로 다루어야 한다. 안정적인 고속 이동은 특정 보행 패턴 자체에서 발생하는 것이 아니라 예측, 접촉, 에너지 전달(Energy Transfer), 상태 추정, 실시간 피드백(Real-Time Feedback)이 정확하게 협응될 때 구현된다.

## 03.09. RL Learned Gait Policy with Gait Commands [w/Code]

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

강화학습(Reinforcement Learning)은 각각의 이동 모드마다 별도로 설계된 제어기를 요구하는 대신, 명시적인 보행 명령(Gait Command)에 따라 여러 종류의 4족 로봇 보행(Quadruped Gait)을 생성하는 통합 이동 정책(Unified Locomotion Policy)을 구현할 수 있다. 정책(Policy)은 로봇 상태, 이동 명령(Motion Command), 보행 사양(Gait Specification)을 관측하고 관절 목표값(Joint Target), 토크(Torque) 또는 기타 저수준 행동(Low-Level Action)을 출력한다. 시뮬레이션과의 반복적인 상호작용을 통해 설계된 보상(Reward)을 최대화하는 협응된 접촉과 몸체 움직임을 학습한다.

보행 명령(Gait Command)은 목표 전진 속도, 횡방향 속도, 요 속도(Yaw Velocity) 이상의 추가적인 정보를 제공한다. 보행 유형(Gait Type), 발걸음 주파수(Stepping Frequency), 듀티 팩터(Duty Factor), 위상 오프셋(Phase Offset), 몸체 높이(Body Height), 목표 발 여유 높이(Desired Foot Clearance) 특성 등을 지정할 수 있다. 따라서 정책은 얼마나 빠르게 어느 방향으로 움직여야 하는지만 학습하는 것이 아니라, 특정 다리 협응 패턴(Leg Coordination Pattern)을 통해 요청된 움직임을 어떻게 구현해야 하는지도 학습한다.

유용한 표현 방법 중 하나는 걷기(Walk), 트로트(Trot), 페이스(Pace), 바운드(Bound)와 같은 이산적인 레이블 대신 연속적인 위상 매개변수(Continuous Phase Parameter)를 이용하여 보행 명령을 표현하는 것이다. 각 다리에는 정규화된 보행 주기(Normalized Gait Cycle) 내의 위상이 할당되며, 상대적인 위상 오프셋은 네 다리 사이의 협응을 정의한다. 듀티 팩터는 주기 가운데 입각(Stance)에 해당하는 비율을 결정하고, 주파수는 위상 진행(Phase Progression)을 제어하여 다양한 주기적 접촉 패턴을 공통 명령 인터페이스(Common Command Interface)로 표현할 수 있게 한다.

이산적인 보행 레이블(Discrete Gait Label)은 사용자 또는 작업 계획(Task Planning) 수준에서는 여전히 유용할 수 있다. 트로트와 같은 명령은 학습된 정책에 입력되기 전에 사전에 정의된 위상 관계(Phase Relationship), 듀티 팩터, 주파수 범위로 변환될 수 있다. 이를 통해 의미론적 보행 선택(Semantic Gait Selection)과 저수준 협응(Low-Level Coordination)을 분리할 수 있다. 또한 상위 수준 소프트웨어가 서로 다른 이동 행동을 요청하더라도 정책 아키텍처(Policy Architecture)를 변경하지 않고 유지할 수 있다.

관측 벡터(Observation Vector)는 일반적으로 몸체 자세(Body Orientation), 각속도(Angular Velocity), 추정 선속도(Estimated Linear Velocity), 관절 위치(Joint Position), 관절 속도(Joint Velocity), 이전 행동(Previous Action), 명령 변수(Command Variable)를 포함한다. 일부 정책은 접촉 상태(Contact State), 지형 측정값(Terrain Measurement), 발 위치(Foot Position), 국부 높이 샘플(Local Height Sample)을 추가로 입력받는다. 가능한 경우 관측값은 몸체 중심 좌표계(Body-Centered Coordinate)로 표현하여 학습된 행동이 절대적인 세계 좌표 위치나 방향에 불필요하게 의존하지 않도록 한다.

위상 정보(Phase Information)는 명령 조건부 보행 학습(Command-Conditioned Gait Learning)에 특히 유용하다. 정책은 현재 보행 위상을 사인(Sine)과 코사인(Cosine)으로 인코딩한 값을 입력받을 수 있으며, 이를 통해 주기 경계(Periodic Boundary)를 연속적으로 표현할 수 있다. 이후 개별 다리의 위상은 전역 위상(Global Phase)과 명령된 오프셋으로부터 계산할 수 있다. 이를 통해 신경망(Neural Network)은 전체 보행 시계(Gait Clock)를 과거 정보에서 직접 추론하지 않고도 각 다리가 언제 입각 또는 유각(Swing)에 진입해야 하는지에 대한 명시적인 시간 기준을 얻는다.

행동(Action)은 하위 수준 비례-미분 제어기(Proportional-Derivative Controller)를 위한 목표 관절 위치(Desired Joint Position)로 표현할 수 있다. 이러한 구성에서는 강화학습이 협응된 자세와 다리 움직임을 결정하는 동안 기존의 피드백 루프(Feedback Loop)가 높은 대역폭의 관절 안정화(Joint Stabilization)를 제공한다. 다른 시스템에서는 관절 토크를 직접 예측하거나 모델 기반 명령(Model-Based Command)에 대한 잔차 보정(Residual Correction)을 출력한다. 행동 표현(Action Representation)은 학습 난이도, 강건성(Robustness), 그리고 학습된 정책에 부여되는 제어 권한(Control Authority)에 큰 영향을 미친다.

보상 함수(Reward Function)는 훈련 과정에서 어떤 이동 특성이 나타날지를 결정한다. 속도 추종 항(Velocity-Tracking Term)은 로봇이 명령된 선속도와 각속도를 따르도록 유도하고, 자세 및 몸체 높이 항은 자세를 조절한다. 과도한 토크, 관절 가속도, 행동 변화(Action Change), 발 미끄러짐(Foot Slip), 충돌(Collision), 바람직하지 않은 몸체 접촉을 억제하기 위한 페널티(Penalty)를 추가할 수 있다. 이러한 항의 상대적인 가중치(Relative Weight)는 결과 행동이 정밀도, 부드러움, 효율성, 강건성 가운데 무엇을 우선하는지를 결정한다.

보행별 보상(Gait-Specific Reward)을 이용하면 요청된 접촉 패턴을 유도할 수 있다. 명령된 위상과 듀티 팩터로부터 목표 접촉 스케줄(Desired Contact Schedule)을 생성하고, 정책이 예상되는 입각 및 유각 상태를 일치시킬 때 보상을 제공할 수 있다. 발 힘(Foot Force) 또는 발 속도(Foot Velocity)에 관한 항을 이용하여 지지 접촉과 움직이는 발을 구분할 수도 있다. 이러한 보상 설계(Reward Shaping)는 정책이 물리적 안정성을 유지하기 위해 필요한 경우 일정한 편차를 허용하면서도 명확하게 인식 가능한 명령 보행을 학습하도록 돕는다.

그러나 지나치게 엄격한 접촉 보상(Contact Reward)은 강건성을 감소시킬 수 있다. 외란(Disturbance)이 발생한 로봇은 명령된 시점보다 발을 일찍 내려놓거나 명목 스케줄보다 입각을 더 오래 유지해야 할 수 있다. 보상 함수가 모든 타이밍 편차를 강하게 처벌하면 정책은 균형을 희생하면서 이상적인 보행 패턴을 유지하려 할 수 있다. 따라서 실제적인 훈련에서는 보행 일치성(Gait Conformity), 작업 성능(Task Performance), 복구(Recovery) 사이의 균형을 조절하여 명령 타이밍을 안전하지 않은 절대 규칙이 아니라 강한 선호 조건으로 사용한다.

훈련 과정에서의 명령 샘플링(Command Sampling)은 범용적인 정책을 얻는 데 매우 중요하다. 목표 속도, 요 회전율(Yaw Rate), 보행 주파수, 위상 오프셋, 듀티 팩터를 에피소드(Episode) 간 또는 에피소드 내부에서 무작위화할 수 있다. 훈련 분포(Training Distribution)는 실제 운용에서 예상되는 조합을 포함하면서 물리적으로 불가능한 넓은 영역은 피해야 한다. 점진적 커리큘럼(Progressive Curriculum)은 단순한 저속 명령에서 시작하여 점차 빠르고 다양하며 더욱 동적인 보행 구성으로 확장할 수 있다.

훈련 중 명령 매개변수를 연속적으로 변화시키면 학습된 보행 사이의 부드러운 전환(Smooth Transition)이 자연스럽게 나타날 수 있다. 독립적인 트로트와 바운드 동작만 훈련하는 대신 정책이 위상 오프셋, 주파수, 듀티 팩터의 점진적인 변화를 경험하도록 할 수 있다. 그러면 정책은 명목 보행들을 연결하는 중간 협응 패턴(Intermediate Coordination Pattern)을 학습한다. 이를 통해 가능한 모든 보행 전환을 위한 대규모 수작업 유한 상태 기계(Finite-State Machine)의 필요성을 줄일 수 있다.

실제 시스템에서는 가속, 정지, 회전 또는 보행 변경에 대한 갑작스러운 요청이 발생할 수 있으므로 급격한 명령 변화(Abrupt Command Change) 역시 훈련 과정에 포함해야 한다. 정책은 명령된 보행을 항상 순간적으로 구현할 수 있는 것은 아니라는 사실을 학습해야 한다. 동적 상태(Dynamic State), 현재 접촉, 사용 가능한 액추에이터 제어 능력이 전환 속도를 결정한다. 명령 변화가 포함된 훈련을 통해 신경망은 상위 수준 요청과 로봇의 물리적 연속성(Physical Continuity)을 조정하는 방법을 학습한다.

도메인 랜덤화(Domain Randomization)는 학습된 보행 정책을 시뮬레이션에서 실제 하드웨어로 전이(Sim-to-Real Transfer)하는 능력을 향상시킨다. 로봇 질량, 무게중심 위치, 링크 관성(Link Inertia), 모터 출력, 관절 마찰(Joint Friction), 지면 마찰, 센서 잡음(Sensor Noise), 통신 지연(Communication Delay), 지형 특성을 훈련 과정에서 변화시킬 수 있다. 이러한 다양한 조건에서 성공하는 정책은 완벽하게 보정된 단일 시뮬레이션 모델에 의존할 가능성이 낮아진다.

액추에이터 모델링(Actuator Modeling)은 동적 이동(Dynamic Locomotion)에서 특히 중요하다. 비현실적으로 즉각적인 토크 또는 위치 응답을 허용하면 시뮬레이션 정책이 실제 모터에서는 재현할 수 없는 행동을 이용할 수 있다. 훈련에서는 토크 한계(Torque Limit), 속도 한계(Velocity Limit), 제어 지연(Control Latency), 감속기 효과(Gearbox Effect), 근사적인 모터 동역학(Motor Dynamics)을 고려해야 한다. 행동 필터링(Action Filtering)이나 지연 행동 모델(Delayed-Action Model)을 사용하면 시뮬레이션 명령과 실제 하드웨어 실행 사이의 차이를 추가로 줄일 수 있다.

지형 랜덤화(Terrain Randomization)는 보행 정책을 평지 이동 이상으로 확장할 수 있다. 높이 변화, 경사면, 계단, 순응성 표면(Compliant Surface), 마찰 변화를 통해 정책이 접촉 타이밍과 몸체 움직임의 다양한 외란을 경험하도록 할 수 있다. 선제적 적응(Anticipatory Adaptation)이 필요한 경우 지형 관측 정보를 명시적으로 제공할 수 있다. 외부수용성 정보(Exteroceptive Information)가 없더라도 정책은 고유수용성(Proprioception)을 통해 반응형 강건성을 학습할 수 있지만, 아직 몸체에 영향을 주지 않은 장애물을 신뢰성 있게 예측할 수는 없다.

특권 정보(Privileged Information)는 실제 운용에서는 사용할 수 없더라도 훈련 과정에서 유용하게 사용할 수 있다. 교사 정책(Teacher Policy)은 시뮬레이터로부터 정확한 지형 형상, 접촉력, 외부 교란, 실제 몸체 속도를 관측할 수 있다. 이후 학생 정책(Student Policy)은 모방학습(Imitation Learning)이나 비대칭 액터-크리틱(Asymmetric Actor-Critic) 방법을 통해 실제 탑재 센서에서 얻을 수 있는 관측값만으로 동작하도록 학습할 수 있다. 이러한 접근법은 실제 운용 가능한 센싱 요구조건을 유지하면서 학습 과정을 단순화할 수 있다.

순환 신경망(Recurrent Neural Network)이나 관측 이력(Observation History)은 로봇 상태가 부분 관측 가능(Partially Observable)한 경우 도움이 될 수 있다. 관절 움직임, 관성 측정값, 행동, 접촉에 대한 짧은 이력에는 단일 관측값에서 얻기 어려운 속도, 지형 상호작용, 액추에이터 응답에 관한 정보가 포함된다. 따라서 메모리(Memory)는 외란 제거와 적응 능력을 향상시킬 수 있지만, 동시에 훈련과 검증 과정을 복잡하게 만든다.

학습된 보행 정책은 전체 명령 보행 범위에서 관절 및 작업 공간 한계(Joint and Workspace Limit)를 준수해야 한다. 높은 발걸음 주파수나 극단적인 위상 관계는 사용 가능한 다리 속도 또는 도달 범위를 초과하는 발 움직임을 요구할 수 있다. 훈련 페널티를 이용하여 관절 한계에 가까워지는 것을 억제할 수 있지만, 명시적인 명령 범위(Command Bound)를 설정하는 것도 중요하다. 명령 인터페이스는 신경망이 모든 불가능한 요청을 해결하기를 기대하기보다 물리적으로 실현 불가능한 것으로 알려진 조합을 거부하거나 포화(Saturation)시켜야 한다.

에너지와 열적 고려사항(Thermal Consideration) 역시 정책 학습에 포함할 수 있다. 토크 페널티, 기계적 동력 페널티(Mechanical-Power Penalty), 또는 이동 비용(Cost of Transport) 목적을 이용하여 경제적인 움직임을 유도할 수 있다. 그러나 순간 토크를 최소화하는 것이 반드시 에너지 소비를 최소화하는 것은 아니다. 고속 동적 보행은 짧은 접촉 시간을 위해 더 큰 최대 힘을 사용할 수 있으므로 전체 보행 주기와 실제 액추에이터 특성을 기준으로 평가해야 한다.

발 미끄러짐(Foot Slip)은 보행 품질을 평가하는 중요한 신호를 제공한다. 입각 발은 하중을 지지하는 동안 지면에 대한 접선 속도(Tangential Velocity)가 이상적으로 낮아야 한다. 미끄러짐을 페널티로 설정하면 특히 다양한 마찰 조건을 포함하는 훈련 환경에서 효율성과 안정성을 향상시킬 수 있다. 그러나 이상적인 무미끄럼(No-Slip) 가정이 위반될 때마다 행동을 즉시 종료하기보다 불가피한 미끄러짐으로부터 복구할 수 있는 충분한 유연성을 정책에 남겨두어야 한다.

외란 훈련(Disturbance Training)은 복구 행동(Recovery Behavior)을 향상시킨다. 무작위 외력(Random Push), 예상하지 못한 속도 변화, 불완전한 접촉, 페이로드(Payload) 변화를 학습 과정에 도입할 수 있다. 정책은 가능한 경우 보행 명령을 계속 따르면서 보정 착지점(Corrective Foot Placement)과 힘 재분배(Force Redistribution) 전략을 학습한다. 강한 외란이 발생하면 명목 접촉 패턴을 일시적으로 벗어난 후 요청된 보행과 다시 동기화할 수 있다.

4족 로봇이 실제 피지컬 AI(Physical AI) 작업을 수행하는 경우 페이로드 변화(Payload Variation)가 중요하다. 추가 질량은 필요한 지면 반력(Ground Reaction Force), 액추에이터 하중, 고유 진동수(Natural Frequency), 몸체 관성(Body Inertia)을 변화시킨다. 훈련 과정에 페이로드 질량과 위치 변화를 포함하면 학습된 정책이 단일 명목 구성에 덜 민감해질 수 있다. 큰 구성 변화가 예상되는 경우에는 명시적인 페이로드 추정값(Payload Estimate)을 추가적인 상황 정보(Context)로 입력할 수도 있다.

상위 수준 내비게이션(Higher-Level Navigation)은 보행 명령 인터페이스를 이용하여 작업과 환경에 따라 이동 행동을 선택할 수 있다. 계획기(Planner)는 불확실한 지형에서는 보수적인 걷기(Conservative Walk)를 요청하고, 규칙적인 지면에서는 트로트를 사용하며, 충분한 공간과 마찰력이 확보되면 더욱 빠른 동적 보행을 요청할 수 있다. 강화학습 기반 제어기는 이러한 의미론적 또는 매개변수화된 명령을 연속적인 전신 행동(Whole-Body Action)으로 변환하므로 내비게이션 계층이 개별 관절 궤적을 직접 관리할 필요가 없다.

학습된 정책이 시뮬레이션과 실제 하드웨어 시험에서 우수한 성능을 보이더라도 안전 계층(Safety Layer)은 여전히 중요하다. 관절 위치, 속도, 토크, 몸체 자세, 접촉력, 온도를 신경망 정책과 독립적으로 감시할 수 있다. 검증된 운용 영역(Validated Operating Region)을 벗어나는 명령은 제한할 수 있으며, 심각한 불안정성이 발생하면 보수적인 복구 또는 정지 행동(Shutdown Behavior)을 실행할 수 있다. 학습은 결정론적 보호 메커니즘(Deterministic Protection Mechanism)을 제거하는 것이 아니라 이동 능력을 확장하는 방향으로 사용되어야 한다.

정책 검증(Policy Validation)은 평균 보상(Average Reward)만을 평가해서는 안 된다. 각각의 명령 보행에 대해 속도 추종, 접촉 타이밍, 몸체 안정성, 발 미끄러짐, 에너지 소비, 최대 토크(Peak Torque), 충격력(Impact Force), 전환 품질(Transition Quality), 외란 복구 성능을 평가해야 한다. 특히 명령 조합(Command Combination)에 대한 시험이 중요하다. 신경망 정책은 명목 훈련 지점에서는 우수하게 동작하더라도 그 사이 또는 훈련 범위를 벗어난 영역에서는 예상하지 못한 행동을 나타낼 수 있기 때문이다.

시뮬레이션-실환경 검증(Simulation-to-Real Validation)은 점진적으로 진행해야 한다. 초기 하드웨어 시험에서는 낮은 속도, 높은 지지 여유(Support Margin), 제한된 보행 명령을 사용한 후 점차 동적 행동으로 범위를 확장할 수 있다. 기록된 관측값, 행동, 접촉 이벤트(Contact Event), 모터 전류(Motor Current), 추종 오차를 분석하면 체계적인 시뮬레이션 불일치(Simulation Mismatch)를 확인할 수 있다. 이러한 측정 결과는 액추에이터 모델, 랜덤화 범위, 보상 설계 또는 정책 재훈련을 개선하는 데 활용할 수 있다.

학습된 정책은 모델 기반 이동(Model-Based Locomotion)을 완전히 대체하지 않고 결합하여 사용할 수도 있다. 모델 예측 제어(Model Predictive Control)는 목표 접촉력이나 몸체 궤적을 제공하고, 강화학습은 잔차 보정, 적응형 착지점 조정(Adaptive Foothold Adjustment), 또는 저수준 관절 행동을 제공할 수 있다. 이러한 하이브리드 아키텍처(Hybrid Architecture)는 명시적인 물리 제약조건과 예측 능력을 복잡한 동역학 및 모델링 오차를 보상하는 학습 능력과 결합한다.

피지컬 AI(Physical AI)의 관점에서 명령 조건부 강화학습(Command-Conditioned Reinforcement Learning)은 이동 의도(Locomotion Intent)를 체화된 행동(Embodied Behavior)으로 변환하는 압축된 매핑(Compact Mapping)을 형성한다. 명령은 목표 움직임과 협응 방식을 지정하고, 정책은 현재의 물리적 상태를 고려하여 이러한 요청을 해석하며, 로봇은 센서와 접촉을 통해 결과가 관측되는 행동을 실행한다. 훈련은 모든 제어 규칙을 수작업으로 지정하는 대신 반복적인 물리적 또는 시뮬레이션 상호작용을 통해 이러한 매핑을 형성한다.

따라서 보행 명령을 사용하는 강화학습 기반 보행 정책(RL-Learned Gait Policy with Gait Commands)은 다중 보행 4족 로봇 이동(Multi-Gait Quadruped Locomotion)을 위한 유연한 프레임워크를 제공한다. 그 효과는 단순히 신경망의 용량(Neural-Network Capacity)에만 의존하는 것이 아니라 명령 표현(Command Representation), 관측값, 행동 인터페이스(Action Interface), 보상 구조(Reward Structure), 시뮬레이션 충실도(Simulation Fidelity), 랜덤화(Randomization), 안전 제약조건, 체계적인 검증에 의해 결정된다. 이러한 구성요소를 통합적으로 설계하면 하나의 정책으로 다양한 보행, 부드러운 전환, 외란 복구, 적응형 이동을 통합된 제어 아키텍처(Unified Control Architecture) 안에서 지원할 수 있다.

## 03.10. Gait Controller Performance Benchmarking [w/Code]

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

게이트 제어기 성능 벤치마킹(Gait Controller Performance Benchmarking)은 4족 보행 제어기가 대표적인 운용 조건 전반에서 안정적이고, 정확하고, 효율적이고, 강건하며, 연산 측면에서 실용적인지 여부를 판단하기 위한 체계적인 방법을 제공합니다. 의미 있는 벤치마크는 단순한 성공적인 전진 운동 이상을 평가해야 합니다. 이는 제어기가 명령을 얼마나 잘 따르고, 접촉을 관리하고, 외란을 배제하고, 하드웨어 한계를 준수하며, 재현 가능한 행동을 유지하는지를 측정해야 합니다.

벤치마킹은 제어기가 작동할 것으로 기대되는 운용 영역(Operating Envelope)을 정의하는 것에서 시작됩니다. 이 영역에는 전진 및 측방 속도, 요율(Yaw Rate), 몸체 높이, 페이로드, 지형 경사, 표면 마찰, 장애물 크기, 보행 유형이 포함될 수 있습니다. 테스트는 명목 조건뿐만 아니라 검증된 한계 근처의 조합도 다루어야 합니다. 명확히 정의된 영역이 없으면 서로 다른 제어기의 성능 결과를 일관되게 비교할 수 없습니다.

속도 추종(Velocity Tracking)은 가장 근본적인 메트릭 중 하나입니다. 명령된 전진, 측방, 요 속도를 시간에 따른 측정된 몸체 운동과 비교합니다. 평균 절대 오차(MAE), 평균 제곱근 오차(RMSE), 정상 상태 오차, 과도 응답을 통해 추종 품질을 정량화할 수 있습니다. 일정 속도에서 잘 작동하는 제어기가 가속이나 회전 중에 불량한 응답을 보일 수 있으므로 계단식 변화(Step Change)와 연속적으로 변화하는 명령을 모두 테스트해야 합니다.

몸체 상태 조절(Body-State Regulation)은 로봇이 이동하는 동안 원하는 높이, 롤, 피치, 그리고 때로는 요 오리엔테이션을 유지하는지 평가합니다. 평균 제곱근 오리엔테이션 오차와 최대 편차는 특히 접촉 전이 중에 유용한 측정값을 제공합니다. 수직 몸체 진동 또한 보행의 부드러움을 나타낼 수 있습니다. 과도한 자세 운동은 평균 속도 추종이 허용 가능한 것으로 보이더라도 부적절한 힘 분배를 드러낼 수 있습니다.

접촉 타이밍(Contact Timing)은 의도한 보행 패턴에 대해 평가되어야 합니다. 측정된 착지 및 이륙 이벤트를 명령된 접촉 스케줄과 비교하여 타이밍 오차, 입각 시간, 유각 시간, 듀티 팩터를 계산할 수 있습니다. 주기적 보행의 경우 네 다리 사이의 위상 관계도 측정할 수 있습니다. 이러한 메트릭은 실제 로봇이 보행 생성기에 의해 가정된 협응 패턴을 실제로 실행하는지 여부를 드러냅니다.

접촉력 성능(Contact-Force Performance)은 운동학적 메트릭이 포착할 수 없는 정보를 제공합니다. 피크 수직력, 접선력, 힘 임펄스, 입각 다리 간의 힘 분배, 힘 변화율을 평가할 수 있습니다. 높은 피크 힘은 거친 착지나 불량한 하중 전달을 나타낼 수 있습니다. 측정된 힘을 계획된 MPC 또는 전신 제어 힘과 비교하는 것은 모델 불일치, 추정기 오차, 또는 하위 수준 추종 한계를 드러낼 수도 있습니다.

발 위치 정확도(Foot-Placement Accuracy)는 지형 인식 보행에서 특히 중요합니다. 측정된 착지 위치를 몸체 또는 세계 좌표계에서 명령된 발판과 비교할 수 있습니다. 종방향, 측방향, 수직방향 오차는 각기 다른 결과를 가져오므로 개별적으로 고려해야 합니다. 계단이나 디딤돌에서는 그렇지 않으면 안정적인 몸체 운동에도 불구하고 작은 오차가 모서리로부터의 가용 안전 여유를 줄일 수 있습니다.

유각 발 추종(Swing-Foot Tracking)은 착지 시점뿐만 아니라 전체 궤적에 걸쳐 평가될 수 있습니다. 위치 오차, 이격 오차, 피크 속도, 피크 가속도, 지형으로부터의 최소 거리가 유용한 지표를 제공합니다. 충돌 이벤트는 명시적으로 기록되어야 합니다. 이러한 측정값은 발판 선택으로 인한 실패와 불충분한 궤적 추종 또는 부적절한 장애물 이격으로 인한 실패를 구분하는 데 도움이 됩니다.

미끄러짐(Slip)은 접촉 품질의 결정적인 측정 기준입니다. 입각 동안 지지 표면에 대한 발의 접선 이동량은 정상적인 미끄러짐 없는 운용 상태에서 작게 유지되어야 합니다. 미끄러짐 거리, 미끄러짐 속도, 미끄러짐 이벤트 횟수, 복구 성공 여부를 기록할 수 있습니다. 여러 마찰 계수에 걸쳐 테스트하면 제어기가 마찰 한계에 얼마나 가깝게 작동하는지, 그리고 힘 할당이 감소된 접지력에 적절히 적응하는지 드러납니다.

지속적인 운용을 목적으로 하는 제어기를 비교할 때는 에너지 효율성(Energy Efficiency)을 측정해야 합니다. 관절 기계 전력을 시간에 대해 통합하여 양의 일과 음의 일을 추정할 수 있으며, 전기적 측정값은 배터리 수준의 에너지 소비를 제공할 수 있습니다. 이동 비용(Cost of Transport)은 에너지를 로봇 중량과 이동 거리로 정규화하여 속도나 구성 전반에 걸친 비교를 가능하게 합니다. 장시간 테스트 동안에는 열적 행동도 고려해야 합니다.

액추에이터 활용도(Actuator Utilization)는 외견상 성공적인 보행이 적절한 제어 여유를 남기는지 여부를 나타냅니다. 피크 및 평균 제곱근 관절 토크, 속도, 가속도, 기계 전력, 모터 전류를 하드웨어 한계와 비교할 수 있습니다. 포화 근처에서 반복적으로 작동하는 제어기는 짧은 테스트가 성공하더라도 취약할 수 있습니다. 따라서 포화 시간과 빈도는 실용적 강건성의 가치 있는 측정값을 제공합니다.

동적 보행에는 추가적인 운동량 관련 평가가 필요합니다. 무게중심 속도, 중심 각운동량, 비행 시간, 착지 속도, 착지 임펄스는 트롯, 바운드, 프롱크, 갤럽 행동을 특성화할 수 있습니다. 주기 간 변동(Cycle-to-Cycle Variation)은 특히 중요한데, 보행이 몇 걸음 동안은 안정적으로 보일 수 있지만 결국 실패로 이어지는 운동량 오차를 점진적으로 누적할 수 있기 때문입니다.

안정성(Stability)은 모든 보행에 대해 단일 메트릭으로 표현되어서는 안 됩니다. 저속 보행은 지지 기하 구조와 무게중심 여유를 사용하여 평가할 수 있는 반면, 동적 보행에는 운동량, 접촉 타당성, 복구 가능성과 관련된 측정값이 필요합니다. 몸체 자세 한계, 예측된 마찰 여유, 실행 가능한 보정 발판은 전통적인 안정성 측정값을 보완할 수 있습니다. 벤치마크는 테스트 대상 보행 역학의 물리적 특성과 일치해야 합니다.

외란 배제(Disturbance Rejection) 테스트는 명목 추종을 넘어 강건성을 평가합니다. 보행 주기의 서로 다른 위상에서 종방향, 측방향 또는 회전 방향으로 통제된 외력을 가할 수 있습니다. 유용한 메트릭에는 복구 가능한 최대 임펄스, 피크 몸체 편차, 복구 시간, 보정 발걸음 수, 명령된 보행의 복원 여부가 포함됩니다. 민감도가 접촉 위상에 따라 크게 달라질 수 있으므로 외란 타이밍을 기록해야 합니다.

페이로드 강건성(Payload Robustness)은 탑재 질량과 명목 무게중심에 대한 질량 위치를 변경하여 평가할 수 있습니다. 벤치마크는 페이로드가 증가함에 따라 추종 저하, 자세 오차, 액추에이터 부하, 에너지 소비, 복구 행동을 측정해야 합니다. 편심 페이로드는 중력 모멘트와 관성 모멘트를 모두 유발하므로 제어기가 힘 분배를 적응시킬 수 있는지 테스트하는 데 특히 유용합니다.

지형 벤치마킹(Terrain Benchmarking)은 통제된 표면에서 점점 더 어려운 기하 구조로 진행되어야 합니다. 평지는 기준 성능을 설정하며, 경사로, 단차, 계단, 거친 지형, 불연속적인 발판은 서로 다른 능력을 테스트합니다. 지형 치수와 표면 특성은 정량적으로 기록되어야 합니다. \'쉬운 지형\' 또는 \'ยาก한 지형\'과 같은 설명은 서로 다른 연구실에서 이를 매우 다르게 해석할 수 있으므로 재현 가능한 비교에 불충분합니다.

계단 벤치마크는 챌판 높이, 디딤판 깊이, 경사각, 계단 폭, 표면 마찰, 계단 수를 명시할 수 있습니다. 성능 측정에는 성공적인 승강 및 하강 속도, 발판 오차, 모서리 여유, 몸체 자세 변화, 접촉 실패, 통과 시간이 포함될 수 있습니다. 약간 변형된 계단 치수로 테스트를 반복하면 제어기가 일반적인 계단 오르기 전략 대신 하나의 기하 구조를 학습하거나 부호화했는지 여부가 드러납니다.

고속 벤치마킹(High-Speed Benchmarking)은 입증된 최고 속도와 지속 가능한 운용 속도를 구분해야 합니다. 짧은 피크 속도 주행은 열 부하, 반복적인 충격, 추정기 드리프트, 또는 액추에이터 포화를 드러내지 못할 수 있습니다. 최고 속도의 여러 비율에서 진행되는 더 긴 시도는 더 유용한 성능 프로필을 제공합니다. 직선으로만 빠르게 달리는 로봇은 실용적 이동성이 제한적이므로 회전 능력도 측정해야 합니다.

보행 전이(Gait Transition)는 정상 상태 보행과 별도로 벤치마킹되어야 합니다. 걷기에서 트롯으로, 트롯에서 바운드로의 전이, 가속, 감속, 정지, 회전 전이는 속도 불연속성, 자세 편차, 접촉 타이밍 오차, 피크 힘, 전이 시간을 사용하여 평가할 수 있습니다. 반복적인 전환 테스트는 각 보행을 독립적으로 테스트할 때 나타나지 않을 수 있는 모드 채터링(Mode-Chattering)이나 동기화 문제를 드러낼 수 있습니다.

강화학습 제어기의 경우 명령 커버리지(Command Coverage)가 중요한 벤치마킹 차원입니다. 테스트는 몇 가지 명목 명령만 평가하기보다 속도, 요율, 보행 주파수, 듀티 팩터, 위상 관계의 검증된 조합을 샘플링해야 합니다. 성능 맵은 추종, 안정성 또는 에너지 효율성이 저하되는 영역을 드러낼 수 있습니다. 분포 외(Out-of-Distribution) 명령은 검증된 운용 조건과 명확히 분리되어야 합니다.

모델 불확실성에 대한 강건성(Robustness to Model Uncertainty)은 시뮬레이션이나 통제된 실험에서 질량, 관성, 마찰, 액추에이터 응답, 센서 노이즈, 지연 시간을 수정하여 조사할 수 있습니다. 경쟁하는 제어기들에 동일한 섭동 세트를 적용해야 합니다. 실제 하드웨어는 수학적 표현과 결코 정확히 일치하지 않으므로 불확실성이 증가함에 따른 성능 저하는 단일 명목 모델에서의 성능보다 더 많은 정보를 제공하는 경우가 많습니다.

상태 추정 강건성(State-Estimation Robustness) 역시 명시적으로 테스트되어야 합니다. 인위적인 지연, 측정 노이즈, 외부 로컬라이제이션의 일시적 상실, 또는 편향된 속도 추정치는 보행이 추정기 품질에 얼마나 강하게 의존하는지 드러낼 수 있습니다. 메트릭에는 추종 저하, 안정성 여유, 복구 시간, 고장 임계값이 포함되어야 합니다. 이러한 테스트는 작은 지연조차도 상당한 예측 오차를 유발할 수 있는 고속 보행에 특히 중요합니다.

연산 성능(Computational Performance)은 제어기 성능의 일부입니다. MPC, 전신 최적화, 인지, 학습된 정책은 지정된 제어 주기 내에 완료되어야 합니다. 평균 실행 시간만으로는 불충분하며, 최대 지연 시간, 상위 백분위 지연 시간, 데드라인 초과, 솔버 반복 횟수, 최적화 실패를 기록해야 합니다. 예측 가능한 타이밍을 가진 약간 덜 최적화된 제어기가 가끔 심각한 연산 초과가 발생하는 제어기보다 더 안전할 수 있습니다.

벤치마킹은 제어기 고장을 인지, 하드웨어, 통신 고장과 구분해야 합니다. 동기화된 상태 추정치, 명령, 접촉 측정값, 관절 데이터, 솔버 상태, 센서 타이밍을 로깅하면 테스트 후 진단이 가능해집니다. 표준화된 고장 분류체계(Failure Taxonomy)는 모든 불성공 시도를 동일하게 다루기보다 미끄러짐, 놓친 발판, 관절 포화, 추정기 발산, 충돌, 솔버 실행 불가능성, 통신 타임아웃과 같은 이벤트를 분류할 수 있습니다.

재현성(Repeatability)은 과학적으로 의미 있는 평가에 필수적입니다. 가장 좋은 시도만을 보고하기보다 변동성을 특성화하기 위해 각 테스트 조건을 충분히 반복해야 합니다. 평균, 표준 편차, 신뢰 구간, 성공률로 반복 실험을 요약할 수 있습니다. 무작위화된 외란 타이밍이나 지형 변형은 벤치마크가 고정된 시퀀스에 맞춰 조정된 제어기를 의도치 않게 우대하는 것을 방지할 수 있습니다.

시뮬레이션 벤치마크는 통제되고 재현 가능한 대량의 실험을 가능하게 하므로 가치가 있습니다. 파라미터를 시스템적으로 변경할 수 있고, 희귀한 고장을 안전하게 발생시킬 수 있으며, Ground-Truth 상태 정보를 사용할 수 있습니다. 그러나 시뮬레이션 결과를 하드웨어 성능과 동등한 것으로 취급해서는 안 됩니다. 접촉 모델링, 액추에이터 동역학, 센서 특성, 구조적 컴플라이언스, 지연 시간은 상당한 시뮬레이션과 실제 간의 차이(Sim-to-Real Gap)를 유발할 수 있습니다.

하드웨어 벤치마킹은 제어기가 이러한 모델링되지 않은 효과를 견뎌내는지 검증합니다. 초기 실험은 보수적인 운용 한계 내에 머물러야 하며 높은 속도, 더 큰 외란, 더 어려운 지형, 더 긴 시간으로 단계적으로 확장되어야 합니다. 안전 장비와 자동 보호 메커니즘은 제어기 고장을 숨기지 않도록 사용되어야 합니다. 따라서 개입 이벤트는 벤치마크 결과의 일부로 기록되어야 합니다.

모델 기반, 학습 기반, 하이브리드 제어기 간의 비교는 가능한 한 동일한 로봇 구성, 명령 프로필, 지형 조건, 평가 메트릭을 사용해야 합니다. 그렇지 않으면 하드웨어, 페이로드, 감지, 테스트 시간의 차이가 결과를 지배할 수 있습니다. 정확성, 효율성, 강건성, 적응성, 연산 능력이 서로 다른 접근 방식을 우대할 수 있으므로 벤치마킹은 하나의 제어기 클래스가 보편적으로 우수하다고 가정하기보다 트레이드오프를 식별해야 합니다.

실용적인 벤치마크는 세부 측정값을 보존하면서 여러 메트릭을 구조화된 스코어카드로 결합할 수 있습니다. 성공률, 추종 정확도, 안정성, 에너지, 피크 부하, 외란 복구, 지형 능력, 연산 신뢰성을 개별 차원으로 보고할 수 있습니다. 단일 종합 점수는 순위 매기기를 단순화할 수 있지만, 한 제어기가 다른 제어기와 다르게 작동하는 이유를 이해하는 데 필요한 세부 메트릭을 결코 대체해서는 안 됩니다.

피지컬 AI(Physical AI) 관점에서 게이트 벤치마킹은 인지, 예측, 제어, 물리적 상호작용, 피드백 사이의 전체 폐루프를 평가합니다. 제어기는 수학적 목적 함수가 최소화될 때뿐만 아니라, 체계화된 로봇이 실제 환경 변동성 하에서 안전하고 유용한 운동을 반복적으로 생성할 때 성공적인 것입니다. 따라서 접촉 결과는 내부 모델과 그에 따른 결정의 품질에 대한 실험적 증거가 됩니다.

게이트 제어기 성능 벤치마킹은 궁극적으로 명령된 행동, 환경 조건, 물리적 실행, 측정 가능한 결과 사이의 재현 가능한 관계를 확립해야 합니다. 추종, 접촉, 안정성, 에너지, 강건성, 지형, 액추에이터, 연산 메트릭을 결합함으로써 개발자는 능력과 고장 경계를 모두 식별할 수 있습니다. 이는 보행 평가를 단편적인 성공 주행의 시연에서 제어기 성능에 대한 체계적인 증거로 전환시킵니다.
