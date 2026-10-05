**Volume 21. Quadruped Robot Software**

# Chapter 07. Reinforcement Learning for Locomotion

## 07.01. RL Locomotion Overview Reward Design Architecture

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

강화학습(Reinforcement Learning, RL) 기반 보행(Locomotion)은 사족보행 로봇(Quadruped Robot)의 제어 문제를 순차적 의사결정 문제(Sequential Decision Problem)로 다룬다. 여기서 정책(Policy)은 로봇과 주변 환경에 대한 관측(Observation)을 안정적이고 민첩한 움직임을 생성하는 행동(Action)으로 변환하는 방법을 학습한다. 모든 접촉 순서(Contact Sequence), 발 디딤 위치(Foothold), 관절 궤적(Joint Trajectory)을 명시적으로 계산하는 대신, 제어기는 시뮬레이션 환경과 반복적으로 상호작용하고 보상함수(Reward Function)로 표현된 수치적 피드백을 이용하여 행동을 개선한다.

일반적인 문제 정의에서는 보행을 상태(State), 관측(Observation), 행동(Action), 상태 전이 동역학(Transition Dynamics), 보상(Reward), 에피소드 종료 조건(Episode Termination Condition)으로 구성된 마르코프 의사결정 과정(Markov Decision Process, MDP)으로 표현한다. 내부 상태에는 베이스 자세(Base Pose), 선속도(Linear Velocity)와 각속도(Angular Velocity), 관절 위치와 속도, 발 접촉 상태, 지형 특성, 액추에이터 상태 등이 포함될 수 있다. 정책은 일반적으로 실제 배치(Deployment) 환경에서도 현실적으로 추정하거나 측정할 수 있는 관측값만 입력받는다.

행동 표현(Action Representation)은 학습 안정성과 실제 배치 동작에 큰 영향을 준다. 정책이 관절 토크(Joint Torque)를 직접 출력할 수도 있지만, 많은 실제 사족보행 시스템에서는 관절 위치 목표값(Joint Position Target), 위치 오프셋(Position Offset), 목표 속도(Desired Velocity), 또는 하위 제어기(Lower-Level Controller)를 위한 파라미터를 생성한다. 위치 목표 행동(Position-Target Action)과 고속 비례-미분 제어기(PD Controller) 또는 임피던스 제어기(Impedance Controller)를 결합하면 학습 기반 움직임 생성과 결정론적 액추에이터 수준 안정화를 효과적으로 분리할 수 있다.

보행 명령(Locomotion Command)은 일반적으로 정책 관측값의 일부로 제공되므로 하나의 정책이 단일 고정 보행이 아니라 다양한 행동을 표현할 수 있다. 목표 전진 및 횡방향 속도, 요 회전율(Yaw Rate), 몸체 높이(Body Height), 보행 관련 명령(Gait-Related Command) 등이 학습된 행동을 조건화할 수 있다. 따라서 최종 제어기는 현재 로봇 상태와 목표 움직임 명령을 입력받아 다리와 몸체의 움직임을 지속적으로 적응시키는 행동을 학습한다.

보상 설계(Reward Design)는 학습 알고리즘에서 성공적인 보행이 무엇인지를 정의한다. 일반적인 목적함수(Objective Function)는 명령 추종(Command Tracking), 안정성(Stability), 에너지 효율(Energy Efficiency), 부드러운 움직임(Smoothness), 접촉 품질(Contact Quality), 안전성(Safety)을 결합한다. 개념적으로 전체 보상은 속도 추종, 요 회전율 추종, 몸체 자세, 발 동작, 토크 사용량, 행동 변화량, 관절 한계 회피, 바람직하지 않은 충돌에 대한 페널티 등의 가중 결합으로 표현할 수 있다.

속도 추종(Velocity Tracking)은 일반적으로 가장 중요한 양의 보상 목표 중 하나이다. 측정된 베이스 속도가 명령 속도에 가까워질수록 정책에 높은 보상이 주어지고, 각속도 추종(Angular Tracking)은 목표 회전 속도를 따르도록 유도한다. 지수형 추종 함수(Exponential Tracking Function)는 목표 근처에서 높은 보상을 제공하면서 의미 있는 오차 범위에 걸쳐 부드러운 기울기(Gradient)를 유지할 수 있어 유용하다. 다만 각 보상 항의 크기는 서로 경쟁하는 다른 목적과의 상대적 관계를 고려하여 조정해야 한다.

안정성 목적(Stability Objective)은 과도한 롤(Roll), 피치(Pitch), 수직 속도(Vertical Velocity), 제어되지 않은 몸체 움직임을 억제한다. 이러한 항들은 정책이 동역학적으로 바람직하지 않은 행동을 이용하여 명령 속도만 달성하는 것을 방지한다. 또한 기준 몸체 높이 또는 자세에서 벗어나는 움직임에 추가 페널티를 부여할 수 있다. 그러나 자세 규제를 지나치게 강하게 적용하면 유용한 동적 움직임까지 억제할 수 있으므로 가속, 회전, 충격, 지형 통과 과정에서 몸체가 자연스럽게 반응할 수 있도록 보상 가중치를 설정해야 한다.

에너지 관련 항(Energy-Related Term)은 불필요하게 공격적인 액추에이터 구동을 줄인다. 토크 크기(Torque Magnitude), 기계적 동력(Mechanical Power), 관절 가속도(Joint Acceleration), 또는 토크와 관절 속도의 조합 등에 페널티를 부여하여 효율적인 움직임을 유도할 수 있다. 부드러움 페널티(Smoothness Penalty)는 정책 행동이 급격하게 변화하는 것도 제한한다. 속도 추종만 학습한 정책은 시뮬레이션에서는 동작하지만 실제 액추에이터에 과도한 부담을 주고 하드웨어 전이 성능을 떨어뜨리는 고주파 또는 고토크 전략을 발견할 수 있기 때문에 이러한 목적은 중요하다.

접촉 인지 보상(Contact-Aware Reward)은 발과 지면이 상호작용하는 방식을 형성한다. 목표 행동에 따라 적절한 입각 시간(Stance Duration), 충분한 스윙 발 높이(Swing-Foot Clearance), 제어된 착지 속도(Landing Velocity), 낮은 접선 방향 미끄러짐(Tangential Slip)을 장려할 수 있다. 무릎, 허벅지 또는 로봇 몸체가 지면과 충돌하는 경우 페널티를 적용하여 물리적으로 바람직하지 않은 해를 방지한다. 다만 발의 타이밍에 대한 지나치게 고정된 가정은 지형 적응성을 감소시킬 수 있으므로 접촉 관련 보상은 다양한 지형 조건과 호환되어야 한다.

종료 조건(Termination Condition) 역시 보상 구조의 중요한 구성 요소이다. 로봇이 넘어지거나, 허용 가능한 몸체 자세 범위를 벗어나거나, 금지된 몸체 접촉이 발생하거나, 복구할 수 없는 상태에 진입하면 에피소드를 종료할 수 있다. 조기 종료(Early Termination)는 의미 없는 상태에 시뮬레이션 자원이 소비되는 것을 막는 동시에 허용할 수 없는 행동을 암묵적으로 정의한다. 그러나 종료 규칙이 지나치게 제한적이면 정책이 복구 가능한 외란이나 어려운 상태를 경험하지 못할 수 있다.

학습 아키텍처(Learning Architecture)는 일반적으로 시뮬레이션(Simulation), 정책 최적화(Policy Optimization), 배치 인터페이스(Deployment Interface)를 분리한다. 수천 개의 시뮬레이션 사족보행 로봇이 병렬로 궤적을 실행하는 동안 근접 정책 최적화(Proximal Policy Optimization, PPO)와 같은 온-정책 알고리즘(On-Policy Algorithm)이 관측, 행동, 보상, 가치 추정(Value Estimate)을 수집할 수 있다. 수집된 궤적은 행동을 생성하는 액터 네트워크(Actor Network)와 학습 과정에서 기대 수익(Expected Return)을 추정하는 크리틱 네트워크(Critic Network)를 업데이트하는 데 사용된다.

액터(Actor)는 일반적으로 투영 중력(Projected Gravity), 베이스 각속도, 관절 위치 오차, 관절 속도, 이전 행동(Previous Action), 움직임 명령 등의 고유수용성 관측(Proprioceptive Observation)을 입력받는다. 보행 문제에 따라 지형 높이와 같은 외부수용성 정보(Exteroceptive Information)를 추가할 수도 있다. 관측 정규화(Observation Normalization)와 일관된 좌표계(Coordinate Frame) 정의는 매우 중요하며, 스케일이나 기준 좌표계가 일관되지 않으면 최적화와 실제 하드웨어 전이 성능이 크게 저하될 수 있다.

크리틱(Critic)은 액터와 동일한 관측값을 사용할 수도 있지만, 시뮬레이션에서는 학습 과정에만 추가 특권 정보(Privileged Information)를 제공하는 비대칭 아키텍처(Asymmetric Architecture)를 사용할 수 있다. 정확한 베이스 속도, 지형 파라미터, 접촉력(Contact Force), 마찰계수(Friction Coefficient) 또는 기타 시뮬레이터 상태를 이용하면 실제 배치 시 해당 정보가 필요하지 않으면서도 가치 추정 성능을 향상시킬 수 있다. 이러한 원리는 이후의 교사-학생(Teacher-Student) 및 특권 학습(Privileged Learning) 아키텍처로 자연스럽게 확장된다.

강화학습은 막대한 양의 상호작용이 필요하고 학습 과정에서 필연적으로 불안정한 행동을 탐색하므로 일반적으로 시뮬레이션에서 학습을 시작한다. 병렬 물리 시뮬레이션(Parallel Physics Simulation)을 사용하면 많은 로봇 인스턴스에서 동시에 경험 데이터를 수집할 수 있다. 초기 자세, 명령, 외란(Disturbance), 지형 조건, 물리 파라미터를 무작위화하면 학습 과정에서 경험하는 상태 분포를 넓히고 특정 명목 시뮬레이션 조건에 대한 의존성을 줄일 수 있다.

커리큘럼 설계(Curriculum Design)는 이러한 탐색 과정을 점진적으로 구성한다. 정책은 먼저 평탄한 지형에서 서기와 저속 명령 추종을 학습한 후 더 높은 속도, 경사면, 계단, 거친 지형, 외부 외란, 낮은 마찰 조건을 경험하도록 확장할 수 있다. 난이도는 학습 진행도 또는 작업 성능에 따라 증가시킬 수 있다. 따라서 커리큘럼 학습(Curriculum Learning)은 보행 능력이 발달하는 과정에서 어떤 경험을 제공할 것인지를 제어함으로써 보상 공학(Reward Engineering)을 보완한다.

실제 사족보행 로봇으로 정책을 전이하기 위해서는 학습 아키텍처가 시뮬레이션-현실 간 격차(Simulation-to-Reality Gap)를 고려해야 한다. 질량(Mass), 관성(Inertia), 마찰(Friction), 모터 강도(Motor Strength), 관절 감쇠(Joint Damping), 센서 잡음(Sensor Noise), 통신 지연(Communication Delay), 제어 지연(Control Latency), 지형 특성을 현실적인 범위에서 무작위화할 수 있다. 특히 명령된 관절 목표나 토크가 단순화된 시뮬레이션에서 가정하는 것처럼 즉각적으로 생성되지 않으므로 액추에이터 동역학(Actuator Dynamics)을 명시적으로 모델링할 필요가 있다.

실제 배치 아키텍처(Deployment Architecture)는 일반적으로 여러 제어 주기(Control Rate)로 동작한다. 학습된 정책은 중간 수준의 주파수에서 실행되어 목표 관절 명령을 생성하고, 하위 모터 제어 루프(Motor-Control Loop)는 이보다 훨씬 높은 주파수로 실행될 수 있다. 상태 추정(State Estimation), 안전 모니터링(Safety Monitoring), 관절 한계 적용, 토크 포화(Torque Saturation), 통신 감시, 비상 동작은 강화학습에 전적으로 맡기지 않고 학습 정책 주변의 결정론적 구성 요소로 유지한다.

이러한 분리는 실제 제품 시스템(Production System)에서 필수적이다. 강화학습은 로봇 제어기 전체가 아니라 보행 스택(Locomotion Stack)을 구성하는 하나의 핵심 요소로 보아야 한다. 정책은 적응형 움직임 행동을 제공하고, 상태 추정기는 신뢰할 수 있는 관측값을 제공하며, 액추에이터 인터페이스(Actuator Interface)는 명령을 실행하고, 안전 계층(Safety Layer)은 위험한 출력을 차단한다. 상위 내비게이션(Navigation) 또는 임무 소프트웨어(Mission Software)는 개별 다리를 직접 제어하지 않고 목표 움직임 명령을 제공한다.

따라서 보상 공학(Reward Engineering), 정책 아키텍처(Policy Architecture), 시뮬레이션 충실도(Simulation Fidelity), 커리큘럼 설계, 액추에이터 모델링(Actuator Modeling), 도메인 무작위화(Domain Randomization)는 서로 결합된 하나의 시스템을 형성한다. 최적화 알고리즘만 개선한다고 해서 더 뛰어난 보행이 보장되는 것은 아니다. 정책은 비현실적인 접촉, 과도한 토크, 부정확한 액추에이터 동역학 또는 시뮬레이터에만 존재하는 관측값을 이용하면서도 시뮬레이션에서 높은 보상을 획득할 수 있다. 성공적인 강화학습 보행을 위해서는 학습 초기부터 실제 배치 제약조건이 학습 목표와 환경에 반영되어야 한다.

따라서 평가는 누적 보상(Accumulated Reward)에만 의존해서는 안 된다. 명령 추종 오차(Command-Tracking Error), 전도율(Fall Rate), 외란 복구(Disturbance Recovery), 전기적 또는 기계적 에너지 소비, 발 미끄러짐(Foot Slip), 최대 토크(Peak Torque), 관절 한계 여유(Joint-Limit Margin), 행동 부드러움(Action Smoothness), 지형 통과 성공률(Terrain Success Rate), 파라미터 변화에 대한 강건성(Robustness) 등이 보다 해석 가능한 평가 지표를 제공한다. 특히 학습 과정에서 사용하지 않은 환경(Unseen Environment)에 대한 검증은 학습 분포를 단순히 기억하는 것과 강건한 보행 능력을 획득하는 것을 구분하기 위해 중요하다.

사족보행 로봇 소프트웨어 아키텍처(Quadruped Robot Software Architecture)에서 이러한 프레임워크는 이후의 근접 정책 최적화 기반 학습(PPO-Based Training), 세부 보상 공학(Reward Engineering), 지형 커리큘럼(Terrain Curriculum), 특권 교사-학생 학습(Privileged Teacher-Student Learning), 액추에이터 및 지연 모델링(Actuator and Delay Modeling), 도메인 무작위화(Domain Randomization), 제로샷 시뮬레이션-현실 전이(Zero-Shot Sim2Real Transfer), 온보드 추론(Onboard Inference), 실제 제품 배치(Production Deployment)를 위한 기반을 제공한다. 이러한 주제들은 강화학습 기반 보행(Reinforcement Learning for Locomotion)을 실제 사족보행 로봇 시스템으로 확장하는 전체 개발 흐름을 구성한다.

## 07.02. PPO for Quadruped Locomotion Isaac Gym [w/Code]

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

근접 정책 최적화(Proximal Policy Optimization, PPO)는 비교적 안정적인 정책 업데이트(Policy Update)와 효율적인 병렬 경험 수집(Parallel Experience Collection)을 결합할 수 있기 때문에 사족보행 로봇 보행(Quadruped Locomotion)에 널리 사용된다. 아이작 짐(Isaac Gym) 학습 아키텍처에서는 수천 대의 가상 사족보행 로봇을 GPU에서 동시에 실행할 수 있으므로 순차적인 CPU 중심 시뮬레이션 없이 대규모 보행 경험을 생성할 수 있다. 이를 통해 수억 또는 수십억 단계의 시뮬레이션 제어가 필요한 동적 행동 학습에 PPO를 실용적으로 적용할 수 있다.

보행 문제(Locomotion Problem)는 연속 제어 마르코프 의사결정 과정(Continuous-Control Markov Decision Process)으로 정의된다. 각 정책 실행 단계(Policy Step)에서 모든 가상 로봇은 현재 상태를 설명하는 관측 벡터(Observation Vector)와 목표 움직임을 지정하는 명령(Command)을 입력받는다. 액터 네트워크(Actor Network)는 이 정보를 연속 행동(Continuous Action)으로 변환하고, 환경은 로봇 동역학을 진행시키면서 접촉과 제약조건을 평가하고 보상(Reward)을 계산한 후 종료 정보와 함께 다음 관측값을 반환한다.

일반적인 관측 벡터에는 베이스 각속도(Base Angular Velocity), 투영 중력(Projected Gravity), 명령된 선속도와 각속도, 기준 관절 구성에 대한 상대 관절 위치, 관절 속도, 이전 정책 행동(Previous Policy Action)이 포함된다. 지형 인지 보행(Terrain-Aware Locomotion)이 필요한 경우에는 추가적인 지형 측정값을 포함할 수 있다. 서로 다른 물리 단위를 가진 값들이 신경망 입력의 조건을 악화시키지 않도록 관측 성분은 일반적으로 스케일링(Scaling) 또는 정규화(Normalization)된다.

정책 행동(Policy Action)은 기준 기립 자세(Nominal Standing Configuration)에 대한 관절 위치 오프셋(Joint Position Offset)을 나타낼 수 있다. 적절한 스케일링을 거친 출력은 하위 비례-미분 제어기(Proportional-Derivative Controller, PD Controller)의 목표 관절 위치로 변환된다. PD 제어기는 위치 및 속도 오차를 시뮬레이터에 적용되는 관절 토크(Joint Torque)로 변환한다. 이러한 아키텍처는 PPO가 액추에이터 수준의 안정화까지 완전히 스스로 학습해야 하는 부담을 줄이면서도 동적인 다리 움직임을 학습할 수 있는 충분한 자유도를 유지한다.

아이작 짐(Isaac Gym)은 로봇 모델, 강체 동역학(Rigid-Body Dynamics), 접촉 계산(Contact Calculation), 환경 상태(Environment State), 정책 관련 텐서(Policy-Related Tensor)를 GPU에 유지할 수 있도록 한다. 따라서 CPU와 GPU 사이의 통신을 최소화하면서 병렬 환경을 진행할 수 있다. 핵심적인 장점은 단순히 렌더링이나 시각화를 빠르게 하는 것이 아니라, 높은 처리량의 물리 시뮬레이션(High-Throughput Physics Simulation)과 텐서 처리(Tensor Processing)를 통해 PPO가 수많은 서로 다른 로봇 인스턴스로부터 대규모 롤아웃 배치(Rollout Batch)를 동시에 수집할 수 있다는 것이다.

롤아웃 수집(Rollout Collection) 과정에서 현재 정책은 일정한 시간 구간(Fixed Horizon) 동안 모든 환경에 대한 행동을 샘플링한다. 각각의 전이(Transition)에는 관측값, 행동, 보상, 종료 플래그(Termination Flag), 정책 로그 확률(Policy Log Probability), 가치 추정값(Value Estimate)이 저장된다. 롤아웃 구간이 완료되면 이러한 궤적(Trajectory)이 학습 배치를 구성한다. 이후 반환값(Return)과 어드밴티지(Advantage)를 계산한 다음 여러 번의 최적화 에포크(Optimization Epoch)를 통해 액터와 크리틱 네트워크(Critic Network)를 업데이트한다.

크리틱(Critic)은 현재 상태 또는 관측에서 예상되는 누적 반환값(Expected Cumulative Return)을 추정하며, 정책 그래디언트(Policy Gradient) 추정의 분산을 줄이는 기준선(Baseline)을 제공한다. 일반화 어드밴티지 추정(Generalized Advantage Estimation, GAE)은 여러 시간 범위에 걸쳐 시간차 정보(Temporal-Difference Information)를 결합하기 위해 일반적으로 사용된다. 할인율(Discount Factor)은 미래 보상의 중요도를 결정하며, GAE 파라미터는 낮은 분산(Low Variance)과 낮은 편향(Low Bias) 사이의 균형을 조절한다.

PPO는 롤아웃을 생성한 기존 정책과 새로운 정책을 비교하는 확률비 목적함수(Probability-Ratio Objective)를 이용하여 액터를 업데이트한다. 정책이 지나치게 크게 변화하도록 허용하는 대신 확률비를 일정한 범위 내에서 클리핑(Clipping)한다. 이러한 클리핑 대리 목적함수(Clipped Surrogate Objective)는 파괴적인 정책 업데이트를 억제하면서도 수집된 샘플에 대해 반복적인 최적화를 수행할 수 있도록 하므로 민감한 접촉 기반 보행(Contact-Rich Locomotion)을 학습하는 데 특히 유용하다.

전체 최적화 목적함수(Optimization Objective)는 일반적으로 클리핑된 정책 손실(Clipped Policy Loss), 크리틱 학습을 위한 가치함수 손실(Value-Function Loss), 탐색을 지원하는 엔트로피 항(Entropy Term)을 포함한다. 각 항의 상대적인 계수는 학습 행동에 상당한 영향을 준다. 지나치게 높은 엔트로피는 정밀한 보행의 형성을 방해할 수 있으며, 탐색이 부족하면 정책이 조기에 수렴할 수 있다. 마찬가지로 액터 아키텍처가 적절하더라도 부정확한 크리틱 학습은 어드밴티지 추정을 불안정하게 만들 수 있다.

보상 계산(Reward Computation)은 각각의 병렬 로봇에 대해 독립적으로 수행된다. 속도와 요 회전율(Yaw Rate) 추종은 주요 작업 보상을 제공할 수 있으며, 수직 움직임, 롤(Roll)과 피치(Pitch) 동작, 토크 사용량, 관절 가속도, 행동 변화량, 발 미끄러짐(Foot Slip), 바람직하지 않은 접촉 및 기타 물리적 특성을 제어하기 위해 페널티를 적용할 수 있다. PPO는 주어진 수치적 목적함수를 최적화하므로 보상 구현은 단순히 에피소드 반환값을 증가시키는 것이 아니라 의도한 보행 행동을 정확하게 표현해야 한다.

환경 초기화(Environment Reset)는 학습 루프(Training Loop)의 중요한 구성 요소이다. 로봇이 넘어지거나, 자세 제한을 위반하거나, 금지된 몸체 부위가 접촉하거나, 에피소드 시간 제한에 도달하면 해당 로봇을 초기화할 수 있다. 정책이 제한된 초기 상태에 의존하지 않도록 초기화 상태에는 자세, 명령, 환경 조건에 충분한 변화를 포함해야 한다. 효율적인 GPU 기반 초기화(GPU-Side Reset)를 사용하면 실패한 환경만 다시 시작하면서 나머지 병렬 시뮬레이션을 중단 없이 계속 실행할 수 있다.

명령 샘플링(Command Sampling)은 학습된 제어기가 수행할 수 있는 행동 범위(Behavioral Envelope)를 결정한다. 각 환경에는 무작위로 샘플링된 전진 속도, 횡방향 속도, 요 회전율 명령을 제공할 수 있으며, 이러한 명령은 일정 시간 동안 유지된 후 변경된다. 서로 다른 명령을 가진 다수의 환경을 동시에 학습함으로써 PPO는 각각의 행동에 별도의 네트워크를 사용하지 않고도 가속, 감속, 회전, 횡방향 이동, 정지를 수행할 수 있는 명령 조건형 보행 정책(Command-Conditioned Locomotion Policy)을 학습한다.

지형(Terrain) 역시 병렬 환경 전체에 분산하여 구성할 수 있다. 일부 로봇은 평탄한 지면에서 학습하는 동안 다른 로봇은 경사면, 거친 표면, 단차 또는 절차적으로 생성된 높이장(Procedurally Generated Height Field)을 경험할 수 있다. 지형 난이도는 커리큘럼 로직(Curriculum Logic)을 이용하여 조절할 수 있으므로 성공적인 로봇은 점차 어려운 조건으로 진행한다. 이를 통해 학습 초기에는 지나치게 어려운 지형이 학습을 방해하지 않도록 하면서 최종적으로는 광범위한 보행 환경에 정책을 노출할 수 있다.

도메인 무작위화(Domain Randomization)는 각각의 아이작 짐 환경에 독립적으로 적용할 수 있다. 로봇 질량, 무게중심(Center of Mass), 마찰, 모터 강도, 관절 파라미터, 초기 상태, 외란(Disturbance) 및 기타 물리적 특성을 가상 로봇마다 다르게 설정할 수 있다. 따라서 하나의 PPO 업데이트에 서로 조금씩 다른 로봇 동역학에서 수집한 경험을 포함할 수 있으며, 이를 통해 특정하게 정밀 보정된 하나의 시뮬레이션 모델에 대한 정책 의존성을 줄일 수 있다.

외부 교란(External Perturbation)은 복구 행동(Recovery Behavior)을 학습하는 데 유용하다. 무작위 밀기(Random Push) 또는 일시적인 베이스 속도 교란을 학습 과정에 적용하면 정책이 정상적인 주기적 보행에서 벗어난 상태를 경험할 수 있다. 로봇은 이러한 상황에서도 명령 속도를 계속 추종하면서 균형을 회복해야 한다. 그러나 학습 초기에 지나치게 강한 교란을 적용하면 학습 신호를 압도할 수 있으므로 교란의 크기와 발생 빈도를 신중하게 설정해야 한다.

제어 주파수(Control Frequency)와 시뮬레이션 주파수(Simulation Frequency)는 명확하게 구분해야 한다. 물리 시뮬레이션은 작은 시간 간격(Simulation Time Step)으로 적분할 수 있지만, 학습된 정책은 행동 디시메이션(Action Decimation)을 통해 더 낮은 주파수로 실행할 수 있다. 정책 업데이트 사이에서는 하위 제어기가 여러 번의 물리 시뮬레이션 단계에 걸쳐 명령을 반복적으로 적용한다. 이러한 구조는 모터 제어가 신경망 추론보다 빠르게 동작하는 실제 배치 아키텍처와 유사하며 학습 과정에서 불필요한 정책 평가를 줄인다.

PPO 보행을 위한 신경망 아키텍처(Neural-Network Architecture)는 최종적으로 온보드 시스템에서 결정론적인 지연시간(Deterministic Latency)으로 추론해야 하므로 비교적 간결하게 구성되는 경우가 많다. 다층 퍼셉트론(Multilayer Perceptron, MLP)은 관측 벡터를 행동 분포(Action Distribution)와 가치 추정값으로 효율적으로 변환할 수 있다. 액터는 일반적으로 연속 행동 분포의 평균과 학습되거나 파라미터화된 행동 분산(Action Variance)을 예측하여 학습 중 확률적 탐색을 수행하고 평가 시에는 결정론적 또는 낮은 분산의 행동을 선택할 수 있도록 한다.

학습 진단(Training Diagnostics)에서는 평균 에피소드 보상만 확인해서는 안 된다. 개별 보상 항, 에피소드 길이, 명령 추종 오차, 종료 원인, 행동 크기, 토크 사용량, 정책 엔트로피(Policy Entropy), 가치 손실(Value Loss), 클리핑 비율(Clipping Fraction), 근사 정책 발산(Approximate Policy Divergence)을 함께 분석하면 학습이 성공하거나 실패하는 원인을 파악할 수 있다. 전체 보상이 증가하더라도 과도한 토크나 불안정한 몸체 움직임을 이용해 속도 추종 성능만 향상되는 것과 같은 바람직하지 않은 보상 항 간의 상쇄 현상이 숨겨질 수 있다.

따라서 확률적 학습(Stochastic Training)과 함께 주기적인 결정론적 평가(Deterministic Evaluation)를 수행하는 것이 유용하다. 평가 환경에서는 탐색 잡음(Exploration Noise)을 제거하고 고정된 명령 프로파일, 지형 시퀀스, 외란 시험을 실행할 수 있다. 서로 다른 체크포인트(Checkpoint)의 결과를 비교하면 학습 반환값의 증가가 실제로 의미 있는 보행 성능 향상으로 연결되는지 확인할 수 있다. 체크포인트 저장은 불안정한 업데이트로부터 복구할 수 있게 하며 서로 다른 보상, 무작위화 범위 또는 네트워크 구성을 적용해 학습한 정책을 이후 비교할 수 있도록 한다.

결과적으로 아이작 짐(Isaac Gym)을 이용한 실용적인 PPO 작업 흐름은 대규모 병렬 시뮬레이션(Massively Parallel Simulation), 롤아웃 수집(Rollout Collection), 어드밴티지 추정(Advantage Estimation), 클리핑 정책 최적화(Clipped Policy Optimization), 크리틱 학습(Critic Learning), 평가(Evaluation), 체크포인트 저장(Checkpointing)이 반복되는 폐루프(Closed Loop)를 형성한다. 이러한 구현은 이후의 보상 공학(Reward Engineering), 지형 커리큘럼(Terrain Curriculum), 특권 학습(Privileged Learning), 액추에이터 모델링(Actuator Modeling), 도메인 무작위화(Domain Randomization), 시뮬레이션-현실 전이(Sim2Real Transfer), 온보드 추론(Onboard Inference), 실제 제품 배치(Production Deployment)를 위한 계산 기반을 제공한다.

## 07.03. Reward Engineering Velocity Tracking Energy Style [w/Code]

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

보상 공학(Reward Engineering)은 강화학습 기반 보행(Reinforcement-Learning Locomotion)에서 가장 영향력이 큰 설계 과정 중 하나이다. 정책(Policy)은 궁극적으로 좋은 보행이라는 추상적인 개념이 아니라 수치로 정의된 목적함수(Numerical Objective)를 최적화하기 때문이다. 사족보행 로봇(Quadruped Robot)의 보상은 명령 추종(Command Tracking), 동적 안정성(Dynamic Stability), 에너지 효율(Energy Efficiency), 접촉 품질(Contact Quality), 부드러운 움직임(Smooth Motion), 원하는 보행 특성(Gait Characteristics)을 동시에 표현하면서 시뮬레이터를 악용하는 의도하지 않은 해를 방지해야 한다.

실용적인 보상함수(Reward Function)는 일반적으로 각 정책 실행 단계(Policy Step)에서 평가되는 여러 항의 가중합(Weighted Sum)으로 구성된다. 양의 보상 항(Positive Reward Term)은 원하는 행동을 장려하고, 페널티(Penalty)는 바람직하지 않은 움직임이나 과도한 제어 노력을 억제한다. PPO는 모든 보상, 페널티, 종료 조건(Termination Condition), 명령 분포(Command Distribution)가 함께 형성하는 최적화 공간에 반응하기 때문에 각 구성 요소의 절대적인 크기보다 상대적인 크기가 더 중요할 수 있다.

속도 추종(Velocity Tracking)은 명령 조건형 보행(Command-Conditioned Locomotion)의 주요 작업 목표를 제공한다. 로봇은 목표 전진 및 횡방향 속도를 재현하면서 명령 변화에 민감하게 반응해야 한다. 추종 보상(Tracking Reward)은 명령된 베이스 속도와 측정된 베이스 속도의 차이를 기반으로 구성할 수 있으며, 일반적으로 오차가 0에 가까울 때 높은 값을 제공하고 추종 오차가 증가함에 따라 부드럽게 감소하는 지수 함수(Exponential Function)를 사용할 수 있다.

요 회전율 추종(Yaw-Rate Tracking)은 동일한 원리를 회전 운동으로 확장한다. 수직축을 중심으로 측정된 각속도(Angular Velocity)가 명령된 요 회전율에 가까워질수록 정책에 높은 보상이 주어진다. 로봇이 회전을 달성하기 위해 병진 이동을 희생하거나 전진 속도를 최대화하면서 회전 명령을 무시하지 않도록 선형 및 각속도 추종 항의 균형을 조정해야 한다. 따라서 학습 명령은 실제 배치에서 예상되는 속도와 회전 동작 범위를 충분히 포함해야 한다.

추종 보상은 물리적으로 의미 있는 좌표계(Coordinate Frame)를 기준으로 표현해야 한다. 목표 평면 속도(Planar Velocity)는 일반적으로 로봇 몸체 기준 좌표계(Body-Aligned Frame)에서 표현된 속도와 비교하며, 이를 통해 전역 방향(Global Orientation)에 관계없이 동일한 정책을 사용할 수 있다. 적절한 좌표계 선택은 신경망이 월드 좌표(World Coordinate)에 불필요하게 의존하는 것을 방지하고 무작위화된 환경에서도 전진, 횡방향, 회전 명령의 의미를 일관되게 유지한다.

에너지 효율(Energy Efficiency)은 명시적인 보상 형성(Reward Shaping)이 필요하다. 추종 성능만 보상받는 정책은 불필요하게 공격적인 동작을 발견할 수 있기 때문이다. 일반적인 페널티에는 관절 토크 제곱(Squared Joint Torque), 기계적 동력(Mechanical Power), 관절 속도(Joint Velocity) 또는 이들의 조합이 포함된다. 토크 페널티(Torque Penalty)는 과도한 액추에이터 출력을 억제하고, 동력 관련 항(Power-Related Term)은 부하 상태에서 움직임을 생성하는 데 필요한 에너지 소비를 보다 직접적으로 나타낸다.

에너지 페널티가 보행 목표를 지배해서는 안 된다. 가중치가 지나치게 크면 정책은 제어 노력을 최소화하기 위해 느리게 움직이거나 명령을 무시하거나 외란 복구 능력을 떨어뜨릴 정도로 약한 다리 움직임을 생성할 수 있다. 반대로 가중치가 너무 작으면 로봇은 명령을 정확하게 추종하면서도 높은 토크 피크(Torque Peak)와 비효율적인 진동을 발생시킬 수 있다. 따라서 보상 조정(Reward Tuning)에서는 누적 반환값뿐만 아니라 실제 물리적 성능 지표를 함께 분석해야 한다.

행동 변화율 페널티(Action-Rate Penalty)는 연속된 정책 출력 사이의 급격한 변화를 억제하기 위해 자주 사용된다. 현재 행동이 이전 행동과 크게 다르면 제어기에 그 변화량에 비례하는 페널티를 부여한다. 이는 시간적 부드러움(Temporal Smoothness)을 장려하고 고주파 명령 진동(High-Frequency Command Oscillation)을 감소시킨다. 특히 학습된 위치 목표가 실제 액추에이터에 연결된 고속 비례-미분 제어기(PD Controller)를 통해 실행되는 경우 이러한 항은 중요하다.

관절 가속도(Joint Acceleration) 또는 관절 속도 페널티를 추가적인 정규화(Regularization) 수단으로 사용할 수 있다. 과도한 관절 가속도는 갑작스러운 방향 전환, 충격에 의존하는 움직임 또는 실제 하드웨어에서 재현하기 어려운 시뮬레이터 특화 전략을 나타낼 수 있다. 그러나 이러한 페널티는 동적 보행에 필요한 빠른 다리 움직임을 허용해야 한다. 고속 트로트(Trot), 복구 스텝(Recovery Step), 점프 또는 거친 지형 통과에는 정적인 기립보다 자연스럽게 더 큰 가속도가 필요하다.

스타일 보상(Style Reward)은 단순히 명령 속도를 달성했는지가 아니라 로봇이 작업을 어떠한 방식으로 수행해야 하는지를 정의한다. 원하는 몸체 높이(Body Height), 자세(Orientation), 발 높이(Foot Clearance), 입각 동작(Stance Behavior), 대칭성(Symmetry), 보행 타이밍(Gait Timing), 자세 형태(Posture)를 추가적인 목표로 표현할 수 있다. 이러한 스타일 형성(Style Shaping)은 제약되지 않은 강화학습이 웅크린 보행, 과도한 몸체 진동 또는 불규칙한 스텝과 같이 기술적으로는 성공하지만 기계적으로 바람직하지 않은 움직임을 생성하는 경우에 유용하다.

몸체 자세 페널티(Body-Orientation Penalty)는 일반적으로 중력 방향을 기준으로 롤(Roll)과 피치(Pitch)를 조절한다. 투영 중력(Projected Gravity)은 전역 헤딩(Global Heading) 정보 없이 몸체 자세를 나타낼 수 있으므로 편리한 표현이다. 별도의 수직 속도 페널티(Vertical-Velocity Penalty)는 불필요한 상하 진동을 억제하고, 각속도 페널티(Angular-Velocity Penalty)는 과도한 롤 및 피치 회전율을 감소시킬 수 있다. 이러한 항들은 몸체를 인위적으로 완전히 고정하지 않으면서 안정적인 몸통 움직임을 유도한다.

발 관련 보상 형성(Foot-Related Shaping)은 스윙(Swing)과 입각(Stance) 동작에 영향을 준다. 스윙 발은 지형과 충돌하지 않도록 충분한 높이를 확보하도록 장려할 수 있으며, 입각 발에는 접선 방향 미끄러짐(Tangential Slip)에 대한 페널티를 적용할 수 있다. 접촉력(Contact Force)이나 착지 속도(Landing Velocity)에 대한 페널티는 강한 충격을 줄이는 데 사용할 수 있다. 그러나 발 궤적에 지나치게 엄격한 가정을 적용하면 경사면, 장애물, 느슨한 표면 또는 예상하지 못한 외란에 적응하는 정책의 능력을 제한할 수 있다.

보행 스타일(Gait Style)은 접촉 타이밍(Contact Timing)을 통해서도 형성될 수 있다. 특정 보행 패턴이 필요한 경우 적절한 공중 체류 시간(Air Time), 다리 사이의 위상 관계(Phase Relationship), 특정 접촉 패턴(Contact Pattern)을 장려할 수 있다. 예를 들어 트로트형 보행(Trot-Like Behavior)은 대각선 다리의 협응(Diagonal Coordination)을 장려하여 유도할 수 있다. 그러나 접촉 스케줄(Contact Schedule)을 지나치게 엄격하게 규정하면 속도나 지형 조건에 따라 더 적절할 수 있는 보행 전환이나 대체 전략을 강화학습이 발견하는 능력이 감소한다.

관절 한계 페널티(Joint-Limit Penalty)는 관절 위치 또는 속도 한계에 가까운 상태를 억제하여 기계적 실현 가능성(Mechanical Feasibility)을 보호한다. 명령 토크가 액추에이터 한계에 접근할 때도 유사한 페널티를 적용할 수 있다. 이러한 항은 강제 포화(Hard Saturation) 또는 종료가 필요해지기 전에 부드러운 안전 여유(Soft Safety Margin)를 형성한다. 특히 시뮬레이션에서는 수학적으로 가능하지만 링크 구조, 케이블 배선, 열 부하 또는 실제 액추에이터 제약으로 인해 바람직하지 않은 자세가 허용될 수 있으므로 중요하다.

바람직하지 않은 접촉 페널티(Undesirable Contact Penalty)는 또 다른 중요한 안전 신호를 제공한다. 몸통, 무릎, 상부 다리 또는 기타 접촉이 금지된 로봇 부품이 지면과 접촉하면 강한 음의 보상(Negative Reward)을 적용할 수 있다. 전도(Fall) 또는 심각한 자세 한계 위반이 발생하면 에피소드를 종료할 수도 있다. 연속적인 접촉 페널티와 종료 조건을 함께 사용하면 정책은 복구 가능한 상태 이탈과 완전한 보행 실패를 구분하도록 학습한다.

보상 스케일(Reward Scale)은 제어 시간 간격(Control Time Step)과 함께 해석해야 한다. 매 시뮬레이션 또는 정책 단계마다 누적되는 보상은 시간 스케일링(Time Scaling)을 일관되게 처리하지 않으면 제어 주파수가 변경될 때 수치적으로 달라진다. 이는 서로 다른 실험을 비교하거나 시뮬레이션 아키텍처 사이에서 설정을 이전할 때 중요하다. 따라서 보상 구현에서는 각각의 항이 순간적인 물리량인지, 변화율인지, 또는 시간 적분 비용(Time-Integrated Cost)의 근사값인지 명확하게 정의해야 한다.

보상 클리핑(Reward Clipping)과 정규화(Normalization)는 수치적 안정성을 개선할 수 있지만 좋은 궤적과 매우 우수한 궤적 사이의 의미 있는 차이를 숨길 수도 있다. 마찬가지로 지나치게 큰 음의 페널티는 양의 추종 보상을 압도하여 지나치게 보수적인 행동을 만들 수 있다. 임의의 큰 상수에 의존하기보다는 실제 롤아웃(Rollout)에서 각 보상 항의 크기를 분석하여 대표적인 보행 상태에서 각 항이 의도된 범위로 기여하도록 설계해야 한다.

커리큘럼 학습(Curriculum Learning)과 보상 공학은 강하게 상호작용한다. 학습 초기에는 기본적인 속도 추종과 안정성이 중심이 되고 어려운 지형, 강한 외란, 높은 수준의 명령은 제한될 수 있다. 정책 성능이 향상되면서 더 넓은 명령 범위와 어려운 지형을 적용하면 에너지 효율, 접촉 행동, 보행 스타일의 약점이 나타날 수 있다. 따라서 평탄한 지형에서 적절하게 균형 잡힌 것으로 보였던 보상 항도 전체 학습 분포에서는 다시 평가할 필요가 있다.

효과적인 보상 조정 과정에서는 전체 에피소드 반환값만 관찰하지 않고 각 보상 구성 요소를 개별적으로 기록해야 한다. 속도 오차(Velocity Error), 요 오차(Yaw Error), 토크, 기계적 동력, 행동 변화량, 발 미끄러짐, 몸체 자세, 접촉 이벤트(Contact Event), 종료 원인을 해당 보상값과 함께 모니터링해야 한다. 이를 통해 전체 반환값 향상이 실제 보행 품질 개선을 의미하는지, 아니면 서로 충돌하는 보상 항 사이의 상쇄에 의해 발생했는지를 확인할 수 있다.

보상 제거 실험(Reward Ablation)은 또 다른 효과적인 검증 방법이다. 나머지 학습 설정을 동일하게 유지하면서 특정 보상 항을 제거하거나 가중치를 체계적으로 변경할 수 있다. 이렇게 생성된 정책을 비교하면 어떤 목적이 필수적이고, 중복되며, 또는 의도하지 않게 정책을 제한하는지 확인할 수 있다. 시각적으로 자연스러운 보행이 반드시 낮은 에너지 소비, 강건한 명령 추종 또는 실제 액추에이터로 전이 가능한 동작을 의미하지 않기 때문에 이러한 실험은 특히 중요하다.

최종 보상 아키텍처(Reward Architecture)는 하나의 좁게 최적화된 행동에 의존하지 않으면서 여러 목표를 동시에 만족하는 정책을 생성해야 한다. 정확한 속도 추종은 작업 성능을 제공하고, 에너지 관련 항은 효율적인 액추에이터 구동을 유도하며, 부드러움 관련 항은 실제 구현 가능성을 높인다. 접촉 관련 목적은 지면과의 상호작용을 형성하고, 스타일 관련 항은 기계적으로 바람직한 움직임을 조절한다. 이러한 요소들의 균형이 PPO가 단순히 움직이는 방법만 학습할 것인지, 실제 환경에 강건하게 배치할 수 있는 보행을 획득할 것인지를 결정한다.

따라서 강화학습(Reinforcement Learning) 장의 전체 구조에서 보상 공학은 PPO 학습을 이후의 지형 커리큘럼(Terrain Curriculum), 특권 학습(Privileged Learning), 액추에이터 모델링(Actuator Modeling), 도메인 무작위화(Domain Randomization), 시뮬레이션-현실 전이(Sim2Real Transfer), 온보드 추론(Onboard Inference), 실제 제품 배치(Production Deployment)와 직접 연결한다. 잘 설계된 보상이 이후 단계의 필요성을 제거하는 것은 아니지만, 이후 적용되는 모든 강건성 및 전이 메커니즘이 유지해야 할 핵심 행동 목표(Behavioral Objective)를 확립한다.

## 07.04. Terrain Curriculum for Robust Locomotion [w/Code]

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

지형 커리큘럼 학습(Terrain Curriculum Learning)은 사족보행 로봇(Quadruped Robot)이 학습 초기부터 전체 지형 분포(Terrain Distribution)에 노출되는 대신 점진적으로 더 어려운 지면 조건을 경험하도록 보행 학습을 구성하는 방법이다. 목표는 먼저 기본적인 균형(Balance)과 명령 추종(Command Tracking) 능력을 확립한 후, 안정적인 학습을 유지하면서 경사면, 불규칙한 표면, 장애물, 매우 거친 지형으로 이러한 능력을 확장하는 것이다.

처음부터 어려운 지형에서 학습하면 아직 훈련되지 않은 정책(Policy)이 유용한 보행 상태를 경험하기 전에 넘어질 수 있기 때문에 희소하거나 잘못된 학습 신호가 발생할 수 있다. 커리큘럼(Curriculum)은 정책의 숙련도에 따라 환경 난이도를 조절하여 이러한 문제를 줄인다. 초기 환경에서는 성공적인 스텝이 가능하도록 조건을 제공함으로써 PPO가 더 어려운 상황에 진입하기 전에 몸체 움직임, 관절 행동, 접촉, 보상 사이의 의미 있는 관계를 학습할 수 있도록 한다.

지형 커리큘럼은 일반적으로 단일한 쉬운 단계에서 어려운 단계로 진행하는 방식이 아니라 여러 난이도 차원(Difficulty Dimension)을 정의한다. 지형 거칠기(Terrain Roughness), 경사각(Slope Angle), 단차 높이(Step Height), 장애물 간격(Obstacle Spacing), 표면 불연속성(Surface Discontinuity), 마찰(Friction), 명령 속도(Commanded Velocity), 외란 크기(Disturbance Magnitude)를 각각 변화시킬 수 있다. 따라서 커리큘럼은 다차원적인 보행 과제 분포를 구성하며, 학습 단계에 따라 이 분포의 어떤 영역을 샘플링할 것인지 결정한다.

평탄한 지형(Flat Terrain)은 복잡한 지형 상호작용으로부터 기본적인 보행 동작을 분리할 수 있으므로 유용한 초기 학습 영역을 제공한다. 정책은 기립(Standing), 전진 및 횡방향 속도 추종, 회전, 협응된 스텝(Coordinated Stepping), 몸체 안정화(Body Stabilization), 기본 복구 동작을 학습할 수 있다. 이러한 행동이 안정되면 최적화 과정에서 기본 보행 생성과 어려운 지형 적응을 동시에 발견해야 하는 부담 없이 지형 복잡도를 증가시킬 수 있다.

경사 지형(Sloped Terrain)은 중력 부하(Gravitational Loading)와 접촉력(Contact Force)에 체계적인 변화를 발생시킨다. 오르막에서는 더 큰 추진력과 적절한 몸체 구성이 필요하고, 내리막에서는 제어된 제동과 충격 관리가 요구된다. 커리큘럼 단계에 따라 양의 경사와 음의 경사 각도를 점진적으로 증가시키면 정책은 더욱 불규칙한 3차원 표면을 경험하기 전에 관절 움직임, 입각력(Stance Force), 몸체 자세를 적응시키는 방법을 학습할 수 있다.

거친 지형(Rough Terrain)은 진폭(Amplitude)과 공간 주파수(Spatial Frequency)를 점진적으로 증가시키는 무작위 높이장(Randomized Height Field)을 이용하여 생성할 수 있다. 낮은 난이도에서는 정상적인 보행을 약간만 방해하는 작은 표면 변화가 존재하고, 높은 난이도에서는 불규칙한 발 디딤 위치와 더 큰 몸체 외란이 발생한다. 이러한 점진적 변화는 정책이 현재 발달 중인 복구 능력을 초과하는 장애물을 즉시 경험하지 않으면서 불완전한 접촉과 변화하는 다리 신장 상태에 적응하도록 한다.

단차, 블록, 간격 또는 디딤 구조물과 같은 이산 장애물(Discrete Obstacle)은 연속적인 거친 지형과는 다른 능력을 요구한다. 장애물 높이, 폭, 간격, 배열을 조절하여 난이도를 제어할 수 있다. 복잡도가 증가하면 정책은 더 높은 스윙 발 높이(Swing-Foot Clearance)를 생성하고, 입각 시간(Stance Duration)을 조절하며, 비대칭적인 다리 구성을 허용하고, 기준 지면 높이와 다른 위치에서 발생하는 접촉으로부터 복구해야 한다.

커리큘럼 진행(Curriculum Progression)은 단순한 학습 경과 시간이 아니라 명시적인 성능 기준(Performance Criterion)을 기반으로 결정할 수 있다. 로봇이 요구된 거리를 이동하거나, 명령 추종을 유지하거나, 충분한 에피소드 지속시간을 확보하거나, 특정 성공률(Success Rate)을 달성하면 다음 단계로 진행할 수 있다. 성능 기반 진행은 필요한 능력이 실제로 형성되었는지와 관계없이 일정한 최적화 반복 횟수만으로 환경 난이도가 증가하는 문제를 방지한다.

난이도 하향 조정(Regression)도 동일하게 중요하다. 정책이 현재 지형 단계에서 반복적으로 실패한다면 환경 난이도를 낮추어 다시 유용한 경험을 수집할 수 있는 조건으로 로봇을 이동시킬 수 있다. 양방향 커리큘럼 조정(Bidirectional Curriculum Adjustment)은 실제로 입증된 능력과 학습 분포 사이에 피드백 구조를 형성한다. 또한 다수의 병렬 환경이 반복적인 전도만 발생시키고 유용한 보행 데이터를 거의 생성하지 못하는 상태에 머무르는 것을 방지한다.

대규모 병렬 시뮬레이션(Massively Parallel Simulation)에서는 서로 다른 로봇이 동시에 서로 다른 커리큘럼 단계에 위치할 수 있다. 성공적인 환경은 더 어려운 지형으로 진행하고, 아직 성공하지 못한 환경은 쉬운 단계에 남는다. 이를 통해 이미 확립된 능력과 새롭게 학습해야 하는 과제가 함께 포함된 이질적인 학습 배치(Heterogeneous Training Batch)를 구성할 수 있다. 따라서 PPO는 모든 환경이 동일한 커리큘럼 단계를 거치도록 강제하지 않고 다양한 난이도의 경험을 동시에 학습할 수 있다.

각 난이도 단계에서도 지형 할당(Terrain Assignment)은 충분한 다양성을 유지해야 한다. 하나의 단계에 속한 모든 환경이 동일한 경사면이나 장애물 배열을 사용한다면 정책은 일반적인 지형 강건성(Terrain Robustness)을 획득하는 대신 반복되는 기하학적 패턴을 기억할 수 있다. 절차적 생성(Procedural Generation)을 이용하면 제어된 난이도 범위를 유지하면서 지형 형태를 다양하게 만들 수 있으므로 커리큘럼이 소수의 결정론적인 코스를 암기하는 문제로 축소되는 것을 방지할 수 있다.

명령 난이도(Command Difficulty)는 지형 난이도와 결합할 수 있다. 거친 지면에서의 고속 보행은 동일한 표면을 저속으로 통과하는 것보다 훨씬 어렵기 때문에 어려운 지형에서는 초기 속도와 요 회전율(Yaw Rate) 범위를 보수적으로 제한할 수 있다. 정책의 숙련도가 향상되면 명령 범위를 점차 확대할 수 있다. 이를 통해 지형 적응을 독립적인 문제로 다루는 대신 환경의 기하학적 특성과 보행 요구조건을 함께 변화시키는 통합 커리큘럼을 구성할 수 있다.

보상 공학(Reward Engineering)은 커리큘럼 진행과 호환되어야 한다. 평탄한 지면에서는 적절했던 몸체 움직임, 관절 가속도 또는 기준 보행에서의 편차에 대한 강한 페널티가 어려운 지형에서 필요한 움직임을 억제할 수 있다. 강건한 보상 아키텍처(Reward Architecture)는 필요할 때 더 큰 몸체 및 다리 적응 동작을 허용하면서도 불안정성, 과도한 에너지 소비, 발 미끄러짐, 기계적으로 바람직하지 않은 행동을 계속 억제해야 한다.

지형 커리큘럼은 접촉 관련 보상(Contact-Related Reward)과도 상호작용한다. 장애물 높이가 증가하면 자연스럽게 스윙 궤적(Swing Trajectory), 착지 속도(Landing Velocity), 입각 시간, 접촉력이 변화한다. 발 높이 또는 접촉 타이밍 보상이 지나치게 제한적인 가정을 포함하면 정책은 더 높은 커리큘럼 단계에서 실패할 수 있다. 따라서 보상 항은 모든 지형에서 하나의 고정된 보행 형상을 강제하기보다 유용한 물리적 행동을 표현하도록 설계해야 한다.

고유수용성 보행(Proprioceptive Locomotion)은 명시적인 지형 인식(Terrain Perception)이 없는 경우에도 지형 커리큘럼의 이점을 얻을 수 있다. 접촉 타이밍, 관절 부하, 베이스 가속도, 발 미끄러짐의 다양한 변화를 반복적으로 경험하면 정책은 로봇 내부 측정값을 통해 간접적으로 지형에 반응하는 방법을 학습한다. 따라서 학습된 제어기는 지면과 실제로 상호작용한 이후에만 관측할 수 있는 외란에 대해서도 반응형 적응(Reactive Adaptation) 능력을 획득할 수 있다.

외부수용성 관측(Exteroceptive Observation)을 사용할 수 있다면 지형 커리큘럼 학습은 앞으로 나타날 지형 형상과 적절한 행동 사이의 관계도 학습하도록 한다. 높이 샘플(Height Sample), 깊이 정보에서 추출된 지형 특징, 고도 정보(Elevation Information)는 경사면과 장애물에 대한 사전 정보를 제공할 수 있다. 학습에서 사용하는 관측값이 실제 배치 환경에서 이용 가능한 정보와 유사하다면 커리큘럼 진행을 통해 반응형 복구뿐만 아니라 예측형 적응(Anticipatory Adaptation) 능력도 발달시킬 수 있다.

도메인 무작위화(Domain Randomization)는 지형 커리큘럼을 대체하는 것이 아니라 보완해야 한다. 커리큘럼은 작업 난이도(Task Difficulty)를 제어하고, 무작위화는 해당 작업 내부의 불확실성을 확대한다. 특정 지형 단계에서도 마찰, 페이로드(Payload), 질량 분포(Mass Distribution), 액추에이터 강도(Actuator Strength), 센서 잡음(Sensor Noise), 지연시간(Latency)을 환경마다 다르게 설정할 수 있다. 따라서 정책은 점점 어려워지는 지형을 해결하는 동시에 로봇과 지면의 정확한 물리 파라미터가 불확실하다는 사실도 학습한다.

커리큘럼이 진행되면서 파국적 망각(Catastrophic Forgetting)이 발생하지 않도록 주의해야 한다. 학습이 어려운 지형에만 집중되면 평탄한 지면이나 단순한 명령에 대한 경험이 부족해져 기존 성능이 저하될 수 있다. 쉬운 환경과 어려운 환경을 혼합하여 유지하면 새로운 능력을 추가하면서 기존에 학습된 기술을 보존할 수 있다. 목표는 가장 높은 지형 단계에서만 최대 성능을 달성하는 것이 아니라 광범위한 보행 능력(Broad Locomotion Competence)을 확보하는 것이다.

따라서 커리큘럼 평가 지표(Curriculum Metric)는 단순한 진행 단계 이상의 정보를 포함해야 한다. 지형 통과 성공률(Terrain Completion Rate), 전도 빈도(Fall Frequency), 이동 거리, 명령 추종 오차, 발 미끄러짐, 에너지 소비, 복구 성공률(Recovery Success), 에피소드 지속시간 등을 분석하면 높은 난이도가 실제 강건성 향상으로 이어지는지 확인할 수 있다. 또한 학습에 사용하지 않은 지형 형태를 평가에 포함하여 절차적 생성기 또는 제한된 지형 집합을 단순히 기억한 결과가 아닌지 검증해야 한다.

최종 커리큘럼은 실제 배치(Deployment)에서 예상되는 운용 범위(Operational Envelope)를 포함하면서 정상 조건을 넘어서는 일정한 여유를 확보해야 한다. 산업 검사(Industrial Inspection)를 위한 정책이라면 평탄한 바닥, 램프(Ramp), 계단, 자갈, 불규칙한 야외 지면, 국부적인 장애물에서 안정적으로 동작해야 할 수 있다. 예상되는 거칠기, 경사 또는 외란보다 약간 더 어려운 조건에서 학습하면 강건성을 확보할 수 있지만, 비현실적으로 극단적인 조건은 학습 용량을 소모하고 실제 로봇 임무와 관련 없는 행동을 유도할 수 있다.

결과적으로 지형 커리큘럼 학습은 강화학습(Reinforcement Learning)을 위한 학습 분포 관리 메커니즘(Distribution-Management Mechanism)으로 작동한다. 이는 PPO 최적화에 필요한 충분한 성공 경험을 유지하면서 정책이 언제, 어떠한 방식으로 점점 더 어려운 보행 상태를 경험할 것인지를 결정한다. 전체 장의 구조에서 이러한 과정은 이후의 특권 학습(Privileged Learning), 액추에이터 및 지연 모델링(Actuator and Delay Modeling), 도메인 무작위화(Domain Randomization), 제로샷 시뮬레이션-현실 전이(Zero-Shot Sim2Real Transfer), 온보드 추론(Onboard Inference), 최종 제품 배치(Production Deployment)를 위한 기반을 마련한다.

## 07.05. Privileged Learning Teacher Student Framework [w/Code]

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

특권 학습(Privileged Learning)은 강화학습 기반 보행(Reinforcement-Learning Locomotion)의 근본적인 문제를 해결하기 위한 방법이다. 시뮬레이션에서는 로봇과 환경에 대한 완전한 정보를 얻을 수 있지만, 실제 배치된 로봇은 제한적이고 잡음이 포함된 센서 정보만 관측할 수 있다. 교사-학생 프레임워크(Teacher-Student Framework)는 이러한 추가적인 시뮬레이션 정보를 버리지 않고 학습 과정에서 활용한 후, 그 결과로 얻어진 보행 능력을 현실적인 온보드 관측(Onboard Observation)만으로 동작할 수 있는 학생 정책(Student Policy)으로 전이한다.

특권 정보(Privileged Information)에는 정확한 베이스 속도(Base Velocity), 지형 형상(Terrain Geometry), 접촉력(Contact Force), 마찰계수(Friction Coefficient), 페이로드 특성(Payload Property), 액추에이터 파라미터(Actuator Parameter), 외부 외란(External Disturbance) 또는 실제 배치 과정에서는 신뢰성 있게 측정하기 어려운 기타 시뮬레이터 상태가 포함될 수 있다. 이러한 변수는 움직임 변화의 원인이 지형, 동역학, 접촉 또는 외부 교란 중 어디에서 발생했는지를 정책이 구분할 수 있도록 하므로 학습 과정의 보행 문제를 더욱 쉽게 해석할 수 있게 한다.

교사 정책(Teacher Policy)은 이러한 풍부한 상태 표현(State Representation)에 접근할 수 있는 시뮬레이션 환경에서 학습된다. 교사의 관측값은 일반적인 고유수용성 측정(Proprioceptive Measurement)과 환경 및 로봇 동역학을 설명하는 특권 변수를 결합할 수 있다. 이후 PPO 또는 다른 강화학습 알고리즘은 최종적으로 배치될 제어기에서는 사용할 수 없는 추가 정보를 활용하면서 명령 추종(Command Tracking), 안정성(Stability), 에너지 효율(Energy Efficiency), 지형 통과(Terrain Traversal), 복구 행동(Recovery Behavior)을 최적화한다.

교사는 숨겨진 물리 변수(Hidden Physical Variable)에 직접 접근할 수 있으므로 관측 이력으로부터 이러한 변수를 먼저 추론하지 않고도 효과적인 대응을 학습할 수 있다. 예를 들어 지형 높이나 마찰 정보를 알고 있다면 즉시 발 움직임을 조절할 수 있으며, 외부 외란에 대한 정보를 알고 있다면 적절한 복구 동작을 생성할 수 있다. 따라서 교사는 최종적으로 배치되는 정책이 아니라 풍부한 정보를 활용하는 기준 정책(Reference Policy)의 역할을 수행한다.

학생 정책(Student Policy)은 실제 로봇의 온보드 시스템에서 현실적으로 획득할 수 있는 관측값만 사용하도록 제한된다. 여기에는 관성측정장치(IMU) 측정값, 관절 위치 및 속도, 이전 행동(Previous Action), 명령 속도(Commanded Velocity), 추정된 베이스 움직임, 그리고 필요한 경우 외부수용성 지형 관측(Exteroceptive Terrain Observation)이 포함될 수 있다. 학생은 시뮬레이터에서만 사용할 수 있는 물리량에 직접 접근할 수 없으므로 실제 로봇의 센싱 조건과 유사한 불완전한 정보를 사용하여 유용한 교사 행동을 재현해야 한다.

교사에서 학생으로의 전이(Teacher-to-Student Transfer)는 정책 증류(Policy Distillation), 모방(Imitation) 또는 표현 학습(Representation Learning)의 형태로 구성할 수 있다. 시뮬레이션에서 동일하거나 서로 관련된 상태를 두 네트워크에 제공하고, 학생은 제한된 관측으로부터 교사의 행동 또는 내부 표현을 재현하도록 학습한다. 이를 통해 강화학습 보상에 추가적인 지도학습 신호(Supervised Learning Signal)를 제공할 수 있으며 부분 관측만으로 강건한 보행을 처음부터 발견해야 하는 어려움을 크게 줄일 수 있다.

간단한 증류 목적함수(Distillation Objective)는 교사와 학생 행동 사이의 차이를 최소화한다. 연속적인 사족보행 제어에서는 목표 관절 위치(Desired Joint Position), 행동 평균(Action Mean) 또는 정책 분포(Policy Distribution) 사이의 차이를 사용할 수 있다. 그러나 작은 행동 차이도 미래의 로봇 상태를 변화시키고 결과적으로 학생을 교사가 생성한 궤적에서 경험하지 못했던 상태 영역으로 이동시킬 수 있기 때문에 직접적인 행동 일치(Action Matching)만으로는 충분하지 않을 수 있다.

상호작용형 학생 학습(Interactive Student Training)은 이러한 분포 불일치(Distribution Mismatch)를 줄일 수 있다. 학생이 시뮬레이션 로봇을 직접 제어하도록 허용하면서 교사 또는 특권 크리틱(Privileged Critic)이 학생이 실제로 방문한 상태에 대한 기준 정보를 제공한다. 따라서 학습에는 이상적인 교사 궤적만 재현하는 것이 아니라 학생 자신의 오류로부터 복구하는 과정도 포함된다. 접촉 동역학(Contact Dynamics)은 여러 스텝에 걸쳐 작은 행동 오차를 크게 증폭시킬 수 있기 때문에 이러한 과정은 보행 학습에서 특히 중요하다.

또 다른 접근법은 특권 정보의 잠재 표현(Latent Representation)을 도입하는 것이다. 교사 측 인코더(Teacher-Side Encoder)는 지형, 동역학, 접촉 또는 외란 변수를 압축된 잠재 벡터(Latent Vector)로 변환하고 이를 이용하여 정책 행동을 조건화한다. 이후 학생 측 적응 모듈(Student-Side Adaptation Module)은 관측 가능한 이력으로부터 이에 대응하는 잠재 표현을 추정한다. 따라서 실제 배치 정책은 모든 숨겨진 물리 파라미터를 명시적으로 복원하지 않고도 자신의 행동을 적응시킬 수 있다.

숨겨진 특성을 단일 시점의 관측만으로 추론할 수 없는 경우 관측 이력(Observation History)이 특히 중요하다. 마찰, 페이로드 변화, 액추에이터 성능 저하, 지형 순응성(Terrain Compliance), 제어 지연(Control Delay)은 관절 움직임과 몸체 반응의 시간적 패턴을 통해 나타날 수 있다. 학생은 최근의 여러 관측과 행동을 누적 벡터(Stacked Vector), 순환 신경망(Recurrent Network), 시간 합성곱(Temporal Convolution) 또는 기타 이력 인코더(History Encoder)를 통해 처리하여 잠재적인 물리적 상황을 추정할 수 있다.

특권 크리틱(Privileged Critic)은 이와 관련된 비대칭 아키텍처(Asymmetric Architecture)를 제공한다. 액터(Actor)는 실제 배치와 호환되는 관측값만 입력받지만, 크리틱(Critic)은 학습 과정에서 추가적인 시뮬레이터 상태를 사용할 수 있다. 최종 행동 생성 과정에서는 크리틱이 필요하지 않으므로 실제 배치 정책에 존재하지 않는 센서 의존성을 만들지 않으면서 특권 정보를 이용하여 가치 추정(Value Estimation)을 향상시킬 수 있다. 이는 완전한 특권 교사 정책을 학생에게 전이하는 방법보다 간단한 대안이 될 수 있다.

교사와 학생 아키텍처에서는 학습 전용 데이터(Training-Only Data)와 실제 배치에서 사용 가능한 데이터(Deployment-Available Data)를 명확하게 분리해야 한다. 시뮬레이터 변수가 실수로 학생의 관측에 포함되면 해당 정책은 시뮬레이션 검증에서는 뛰어난 성능을 보이더라도 실제 하드웨어에서는 올바르게 실행할 수 없게 된다. 따라서 관측 인터페이스(Observation Interface)를 명시적인 소프트웨어 계약(Software Contract)으로 관리하고, 특권 채널을 구분하여 실제 제품 추론 경로(Production Inference Path)에 들어가지 않도록 해야 한다.

학생을 학습할 때는 센서 잡음(Sensor Noise)과 상태 추정 오차(Estimation Error)도 표현해야 한다. 완벽한 시뮬레이션 IMU 값, 관절 측정값 또는 베이스 속도 추정값은 변수 이름이 실제 센서와 동일하더라도 또 다른 형태의 특권 정보가 될 수 있다. 따라서 잡음, 바이어스(Bias), 지연시간(Latency), 필터링 효과(Filtering Effect), 관측 누락(Dropped Observation), 추정 불확실성(Estimation Uncertainty)을 모델링하여 학생이 실제 온보드 상태 추정 파이프라인(Onboard State-Estimation Pipeline)에 가까운 조건에서 학습하도록 해야 한다.

지형 정보(Terrain Information) 역시 동일한 원칙에 따라 다루어야 한다. 교사는 로봇 주변의 정확한 지형 높이를 입력받을 수 있지만, 실제 배치된 학생은 깊이 카메라(Depth Camera), 라이다(LiDAR), 고도 지도(Elevation Map)를 사용하거나 명시적인 지형 센싱을 전혀 사용하지 않을 수도 있다. 따라서 학습에서는 이상적인 기하학적 정보와 실제로 구현 가능한 지각 정보(Realizable Perception)를 구분해야 한다. 외부수용성 지각(Exteroception)을 사용할 수 없거나 신뢰성이 낮다면 학생은 고유수용성 상호작용과 관측 이력으로부터 지형의 영향을 추론할 수 있다.

교사 자체도 충분히 넓은 환경 분포(Environment Distribution)에서 학습되어야 한다. 기준 질량, 마찰, 지형, 액추에이터 조건에서만 성공하는 교사는 학생에게 강건한 시범 행동(Robust Demonstration)을 제공할 수 없다. 따라서 교사 학습 이전 또는 학습 과정에서 지형 커리큘럼(Terrain Curriculum)과 도메인 무작위화(Domain Randomization)를 적용하여 학생이 최종적으로 대응해야 하는 다양한 조건에서 기준 행동을 생성하도록 할 수 있다.

학생의 성능은 교사와의 행동 유사도(Action Similarity)만으로 평가해서는 안 된다. 중요한 기준은 여전히 폐루프 보행 성능(Closed-Loop Locomotion Performance)이며, 여기에는 명령 추종 오차, 전도율(Fall Rate), 지형 통과 성공률, 외란 복구(Disturbance Recovery), 에너지 소비, 발 미끄러짐(Foot Slip), 액추에이터 실현 가능성(Actuator Feasibility)이 포함된다. 학생이 개별 시간 단계에서는 교사와 다른 행동을 생성하더라도 제한된 관측 조건에서 동일하거나 더욱 강건한 궤적을 생성할 수 있다.

유용한 검증 절차(Validation Procedure)는 동일한 명령 및 지형 분포에서 특권 교사(Privileged Teacher), 시뮬레이션 학생(Simulated Student), 실제 배치 지향 학생(Deployment-Oriented Student)의 성능을 비교하는 것이다. 이들 사이의 성능 차이는 특권 정보가 제거되었을 때 얼마나 많은 능력이 손실되는지를 나타낸다. 관측 이력, 지형 센싱, 적응 잠재 변수(Adaptation Latent Variable), 특권 크리틱 입력을 각각 제거하는 추가적인 절제 실험(Ablation)을 수행하면 어떤 정보 채널이 보행 강건성에 가장 크게 기여하는지 확인할 수 있다.

특권 학습은 변화하는 로봇 동역학(Robot Dynamics)에 대한 적응도 지원한다. 학습 과정에서 페이로드, 모터 강도, 마찰 또는 지연시간을 무작위화하면 교사는 이러한 파라미터에 대한 직접적인 정보를 활용할 수 있고, 학생은 최근 움직임으로부터 그 영향을 추론하는 방법을 학습할 수 있다. 이를 통해 교사-학생 학습은 단순한 행동 복제(Behavior Cloning)를 넘어 암묵적 온라인 시스템 식별(Implicit Online System Identification)과 적응형 보행(Adaptive Locomotion)을 위한 메커니즘으로 확장된다.

최종 배치 아키텍처(Final Deployment Architecture)에는 추론에 필요한 학생 측 구성 요소만 포함된다. 특정 모듈을 학습이나 진단 목적으로 의도적으로 유지하지 않는 한 시뮬레이터 상태, 특권 지형 레이블(Privileged Terrain Label), 정확한 접촉 물리량, 교사 네트워크는 제거된다. 최종 제어기는 온보드 연산 자원(Onboard Computational Budget) 내에서 실행되어야 하며 학생 학습 과정에서 사용한 것과 동일한 관측 정의, 이력 구조, 정규화(Normalization), 행동 인터페이스(Action Interface)를 사용해야 한다.

강화학습 기반 보행(Reinforcement-Learning Locomotion)의 전체 구조에서 특권 교사-학생 학습(Privileged Teacher-Student Learning)은 풍부한 정보를 이용하는 시뮬레이션 학습과 센서 제약을 갖는 실제 로봇 배치 사이를 연결하는 역할을 한다. 이는 PPO, 보상 공학(Reward Engineering), 지형 커리큘럼을 기반으로 하며, 이후 단계의 액추에이터 및 지연 모델링(Actuator and Delay Modeling), 도메인 무작위화(Domain Randomization), 제로샷 시뮬레이션-현실 전이(Zero-Shot Sim2Real Transfer), 온보드 추론(Onboard Inference), 실제 제품 배치(Production Deployment)를 위한 정책을 준비한다.

## 07.06. Actuator Net Delay and Hardware Modeling [w/Code]

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

액추에이터, 네트워크 지연 및 하드웨어 모델링(Actuator, Network-Delay, and Hardware Modeling)은 강화학습 기반 보행(Reinforcement-Learning Locomotion)에서 필수적이다. 시뮬레이션 정책은 일반적으로 실제 사족보행 로봇이 제공할 수 있는 것보다 더 이상적이고 빠른 구동을 가정하기 때문이다. 실제 모터에는 제한된 대역폭(Bandwidth), 토크 한계(Torque Limit), 마찰(Friction), 전달계 영향(Transmission Effect), 열적 제약(Thermal Constraint), 제어기 동역학(Controller Dynamics)이 존재하며, 센싱과 명령 전달 경로에도 지연시간(Latency)이 발생한다. 이러한 영향을 무시하면 시뮬레이션에서는 우수하지만 실제 하드웨어에서는 불안정한 정책이 생성될 수 있다.

액추에이터 모델(Actuator Model)은 보행 정책이 생성한 행동(Action)과 각 관절에서 실제로 발생하는 기계적 토크(Mechanical Torque) 사이의 관계를 정의한다. 정책이 목표 관절 위치를 출력하는 경우 해당 명령은 일반적으로 모터에 전달되기 전에 하위 비례-미분 제어기(PD Controller) 또는 임피던스 제어기(Impedance Controller)를 통과한다. 결과적인 토크는 정책 명령 자체뿐만 아니라 위치 오차, 속도 오차, 제어기 게인(Controller Gain), 포화 한계(Saturation Limit), 모터 특성 및 전달계 동역학에 의해 결정된다.

단순한 시뮬레이션에서는 비례 및 미분 피드백(Proportional and Derivative Feedback)을 이용하여 관절 토크를 근사할 수 있다. 이러한 표현은 계산 효율이 높고 기본적인 서보 동작(Servo Behavior)을 재현할 수 있지만, 명령과 출력 사이에 이상적인 관계가 존재한다고 가정한다. 실제 액추에이터에는 마찰, 백래시(Backlash), 토크-속도 한계(Torque-Speed Limitation), 전류 포화(Current Saturation), 컴플라이언스(Compliance), 응답 지연(Response Delay)과 같은 비선형 효과가 존재한다. 동적 보행은 저속의 준정적 운동보다 이러한 차이를 훨씬 크게 드러낼 수 있다.

물리적 모터는 무제한의 힘을 발생시킬 수 없으므로 토크 포화(Torque Saturation)를 반드시 모델링해야 한다. 또한 모터 전압과 역기전력(Back Electromotive Force) 제약으로 인해 관절 속도가 증가할수록 사용 가능한 토크가 감소할 수 있다. 시뮬레이션에서 이러한 토크-속도 관계를 무시하면 정책은 실제로 공급할 수 없는 토크가 필요한 고속 관절 움직임을 학습할 수 있다. 이러한 차이는 가속, 충격 복구(Impact Recovery), 등반, 점프, 고속 보행 전환 과정에서 특히 중요해진다.

관절 마찰(Joint Friction)은 이상적인 운동과 실제 운동 사이에 또 다른 차이를 발생시킨다. 쿨롱 마찰(Coulomb Friction), 점성 마찰(Viscous Friction), 정지 마찰(Stiction), 전달 손실(Transmission Loss)은 움직임을 시작하고 유지하는 데 필요한 토크에 영향을 준다. 강화학습을 위해 모든 마찰 특성을 정확한 해석 모델로 식별할 필요는 없지만, 정책이 비현실적으로 마찰이 없는 관절에 의존하지 않도록 이러한 효과의 크기와 변동성을 충분히 재현해야 한다.

컴플라이언스와 전달계 동역학(Transmission Dynamics) 역시 보행에 영향을 줄 수 있다. 기어박스(Gearbox), 벨트(Belt), 구조적 탄성(Structural Elasticity), 직렬 탄성 요소(Series-Elastic Element), 유연한 발(Compliant Foot)은 측정된 관절 위치가 모터 측 움직임과 동적으로 달라지게 할 수 있다. 따라서 액추에이터 모델에는 유효 강성(Effective Stiffness), 감쇠(Damping) 또는 추가적인 내부 상태(Internal State)를 포함할 수 있다. 필요한 모델 복잡도는 이러한 동역학이 학습된 제어기가 사용하는 주파수 영역에 실질적인 영향을 주는지에 따라 결정된다.

모든 비선형 액추에이터 방정식을 수작업으로 구성하는 대신 하드웨어 데이터로부터 액추에이터 네트워크(Actuator Network)를 학습하는 방법도 사용할 수 있다. 명령된 관절 상태, 측정된 관절 상태, 속도, 이전 액추에이터 동작을 신경망 모델의 입력으로 사용하여 실제 토크 또는 액추에이터 응답을 예측할 수 있다. 이러한 액추에이터 네트워크(Actuator Net)는 단순한 PD 모델로 표현하기 어려운 비선형 효과를 근사하면서도 대규모 시뮬레이션에서 사용할 수 있을 정도의 계산 효율을 유지할 수 있다.

액추에이터 네트워크를 위한 학습 데이터(Training Data)는 실제 보행에서 예상되는 운용 영역(Operating Region)을 충분히 포함해야 한다. 실제 로봇이 빠른 트로트(Trotting) 또는 외란 복구(Disturbance Recovery)를 수행한다면 저속 움직임 데이터만으로는 충분하지 않다. 데이터에는 대표적인 관절 위치, 속도, 가속도, 부하 조건, 운동 방향 전환, 명령 진폭(Command Amplitude)이 포함되어야 한다. 그렇지 않으면 학습된 액추에이터 모델이 동적 보행에서 하드웨어 요구가 가장 높은 영역에서 부정확한 외삽(Extrapolation)을 수행할 수 있다.

액추에이터 네트워크는 개념적으로 보행 정책(Locomotion Policy)과 분리되어야 한다. 액추에이터 네트워크의 목적은 보행 제어기를 대체하는 것이 아니라 명령과 실제 액추에이터 동작 사이의 시뮬레이션 매핑을 더욱 현실적으로 만드는 것이다. 강화학습 과정에서 정책은 학습되거나 보정된 액추에이터 모델과 상호작용하며, 실제 로봇에서 해당 행동을 실행하기 전에 보다 현실적인 행동 결과를 경험하게 된다.

지연시간(Latency)도 마찬가지로 중요하다. 정책은 실제 물리 시스템의 상태를 완벽하게 실시간으로 관측하여 즉각적으로 행동하는 것이 아니기 때문이다. 센서 획득(Sensor Acquisition), 필터링(Filtering), 상태 추정(State Estimation), 메시지 전송(Message Transport), 정책 추론(Policy Inference), 명령 전송(Command Transmission), 모터 제어기 처리(Motor-Controller Processing), 액추에이터 응답 각각에서 지연이 발생한다. 빠른 동적 보행에서는 수 밀리초의 지연만으로도 몸체 움직임과 보정 행동 사이의 위상 관계(Phase Relationship)가 달라질 수 있다.

관측 지연(Observation Delay)은 정책이 현재 상태가 아니라 이전 시점의 물리 상태를 나타내는 정보를 입력받는다는 것을 의미한다. 지연된 관성측정장치(IMU) 데이터, 관절 상태 또는 추정 속도를 사용하면 로봇 상태가 이미 상당히 변화한 이후에 보정 행동이 적용될 수 있다. 시뮬레이션에서는 관측 이력(Observation History) 또는 버퍼(Buffer)를 유지하고 가장 최근에 계산된 상태 대신 이전 시간 단계의 데이터를 정책에 전달하여 이러한 효과를 재현할 수 있다.

행동 지연(Action Delay)은 정책 계산과 실제 물리 명령 실행 사이의 시간 간격을 의미한다. 명령은 통신과 하위 제어 처리 과정에서 일정 시간 동안 대기열(Queue)에 머무를 수 있다. 학습 과정에서는 행동 버퍼(Action Buffer)를 사용하여 일정한 수의 시뮬레이션 단계 이후에 명령을 적용함으로써 이를 모델링할 수 있다. 분수 단위 또는 가변 지연(Variable Delay)을 표현하려면 단순한 고정 정수 단계 오프셋 대신 보간(Interpolation), 더 높은 시뮬레이션 주파수 또는 확률적 지연 모델(Stochastic Delay Model)이 필요할 수 있다.

보행 시스템의 구성 요소가 분산 소프트웨어(Distributed Software)를 통해 통신하는 경우 네트워크 지연(Network Delay)을 별도로 모델링할 수 있다. 하위 관절 제어는 일반적으로 로컬에서 결정론적으로 유지하는 것이 바람직하지만, 상태 추정값이나 상위 수준 명령은 미들웨어(Middleware) 또는 네트워크 프로세서를 통해 전달될 수 있다. 이 경우 지연, 지터(Jitter), 패킷 손실(Packet Loss), 스케줄링 변동(Scheduling Variation), 비동기 타임스탬프(Asynchronous Timestamp)가 정책에 제공되는 정보에 영향을 줄 수 있으므로 실제 배치 아키텍처에 따라 이를 고려해야 한다.

고정 지연(Constant Delay) 모델링은 기준 타이밍 예산(Timing Budget)을 설정하는 데 유용하지만 실제 시스템에서는 일반적으로 지터가 존재한다. 정확히 하나의 결정론적 지연시간만 사용하여 학습된 정책은 실제 시스템의 응답이 간헐적으로 더 빠르거나 느려질 때 민감하게 반응할 수 있다. 측정된 범위 안에서 관측 및 행동 지연을 무작위화하면 정책이 타이밍 불확실성(Timing Uncertainty)을 경험하게 되고 예상되는 하드웨어 타이밍 분포에서도 안정성을 유지하는 제어 전략을 학습할 수 있다.

제어 주파수(Control Frequency)는 지연시간과 함께 모델링해야 한다. 정책은 수십 또는 수백 헤르츠(Hz)에서 실행될 수 있는 반면 모터 제어기는 킬로헤르츠(kHz)에 가까운 주파수로 동작할 수 있다. 행동 디시메이션(Action Decimation)을 사용하면 하나의 정책 출력을 여러 물리 적분 단계 동안 유지하고, 그 사이 하위 제어기는 지속적으로 토크를 업데이트한다. 이러한 다중 주기 구조(Multirate Structure)는 실제 온보드 배치에서 사용하려는 타이밍 아키텍처와 최대한 유사하게 구성해야 한다.

하드웨어 모델링(Hardware Modeling)은 액추에이터와 지연시간을 넘어선다. 링크 질량(Link Mass), 관성(Inertia), 무게중심(Center of Mass), 관절 감쇠(Joint Damping), 기계적 한계(Mechanical Limit), 발 형상(Foot Geometry), 접촉 특성(Contact Property), 배터리 상태에 따른 액추에이터 성능, 페이로드(Payload), 센서 장착 상태 등이 모두 보행에 영향을 줄 수 있다. 신뢰할 수 있게 측정된 파라미터는 보정하고, 불확실한 파라미터는 분포(Distribution)로 표현할 수 있다. 목표는 완벽하게 동일한 디지털 복제본을 만드는 것이 아니라 시뮬레이션 오차가 정책이 악용할 수 있는 지름길을 만들지 않도록 하는 것이다.

시스템 식별(System Identification)은 이러한 모델을 구축하는 데 필요한 측정값을 제공한다. 개별 관절에 제어된 명령을 입력하면서 위치, 속도, 전류, 토크 추정값, 타이밍 정보를 기록할 수 있다. 전신 실험(Whole-Body Experiment)을 통해 접촉 및 구조 동역학에 관한 추가 정보를 획득할 수도 있다. 시뮬레이션 응답과 실제 측정 응답을 비교하면 어떤 모델 파라미터 또는 학습된 액추에이터 구성 요소가 보행과 관련된 동작에 가장 큰 영향을 주는지 확인할 수 있다.

하드웨어 로그(Hardware Log)는 명목상의 소프트웨어 주파수에만 의존하지 않고 종단간 타이밍(End-to-End Timing)을 추정하는 데도 사용해야 한다. 타임스탬프가 기록된 센서 획득, 상태 추정기 출력, 정책 실행, 명령 발행, 모터 제어기 수신, 측정된 관절 응답을 분석하면 숨겨진 지연을 발견할 수 있다. 이러한 측정값은 지연 무작위화(Latency Randomization)를 위한 현실적인 범위를 설정하고 통신 지연과 기계적 액추에이터 응답을 구분하는 데 도움을 준다.

모델 검증(Model Validation)은 동일하거나 최대한 유사한 명령 시퀀스를 사용하여 시뮬레이션과 실제 하드웨어를 비교해야 한다. 관절 추종 오차(Joint Tracking Error), 위상 지연(Phase Lag), 토크 응답, 오버슈트(Overshoot), 정착 동작(Settling Behavior), 에너지 소비, 주파수 응답(Frequency Response)이 유용한 평가 지표가 된다. 전신 검증에서는 베이스 가속도, 보행 타이밍, 접촉 이벤트(Contact Event), 복구 동작도 추가로 비교할 수 있다. 정적 관절 위치만 일치시키는 것은 동적 보행용 모델을 검증하기에 충분하지 않다.

액추에이터 및 지연 모델을 불필요하게 복잡하게 만들어서는 안 된다. 병렬 시뮬레이션 처리량을 크게 감소시키는 매우 상세한 모델보다 적절한 무작위화와 결합된 간결한 근사 모델이 실용적으로 더 높은 가치를 제공할 수 있다. 모델 충실도(Model Fidelity)는 보행 정책이 민감하게 반응하는 효과에 집중해야 하며, PPO에 필요한 대규모 경험 생성을 유지하면서 학습 과정에서 정책이 악용할 수 있는 비현실적인 동작을 제거해야 한다.

최종적으로 구성된 학습 환경은 정책을 제한된 액추에이터 성능, 비선형 응답(Nonlinear Response), 현실적인 제어 타이밍, 불확실한 하드웨어 파라미터에 노출시킨다. 이를 통해 시뮬레이션-현실 전이(Sim2Real) 준비 과정은 단순한 기하학적 또는 지형 적응 문제가 아니라 완전한 동적 전이 문제(Dynamic Transfer Problem)로 확장된다. 전체 장의 흐름에서 액추에이터 네트워크(Actuator Network), 지연 및 하드웨어 모델링은 특권 학습(Privileged Learning)을 이후의 도메인 무작위화(Domain Randomization), 제로샷 시뮬레이션-현실 전이(Zero-Shot Sim2Real Transfer), 온보드 추론(Onboard Inference), 실제 제품 배치(Production Deployment)로 연결하는 핵심 단계이다.

## 07.07. Domain Randomization for Quadruped Sim2Real [w/Code]

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

도메인 무작위화(Domain Randomization)는 어떠한 시뮬레이션도 실제 배치된 로봇과 환경의 모든 물리적 특성을 완벽하게 재현할 수 없기 때문에 사족보행 로봇 강화학습(Quadruped Reinforcement Learning)에서 핵심적인 시뮬레이션-현실 전이(Sim2Real) 전략이다. 하나의 기준 모델(Nominal Model)에 대해서만 정책을 최적화하는 대신, 학습 과정에서 불확실한 파라미터를 여러 시뮬레이션 환경에 걸쳐 의도적으로 변화시킨다. 따라서 정책은 하나의 정확한 시뮬레이터 설정을 이용하는 것이 아니라 가능한 동역학 분포 전반에서 효과적인 보행 행동을 학습해야 한다.

기본적인 원리는 모델링 오차(Modeling Error)를 구조화된 불확실성(Structured Uncertainty)으로 다루는 것이다. 로봇 질량, 관성(Inertia), 무게중심(Center of Mass), 관절 마찰(Joint Friction), 모터 강도(Motor Strength), 접촉 특성(Contact Property), 센서 특성, 제어 지연(Control Latency), 지형 파라미터는 모두 시뮬레이션과 실제 하드웨어 사이에서 달라질 수 있다. 학습 과정에서 이러한 값을 샘플링하면 시뮬레이터는 서로 조금씩 다른 다수의 로봇을 생성하며, PPO는 물리적 변화에 견딜 수 있는 행동을 학습하게 된다.

무작위화 범위(Randomization Range)는 임의의 극단적인 값이 아니라 현실적으로 가능한 하드웨어 불확실성을 기반으로 설정해야 한다. 정확하게 측정된 파라미터에는 좁은 범위를 적용할 수 있고, 식별 정확도가 낮은 물리량에는 더 넓은 분포를 사용할 수 있다. 제조 공차(Manufacturing Tolerance), 페이로드 변화(Payload Variation), 배터리 상태, 온도, 기계적 마모(Mechanical Wear), 보정 불확실성(Calibration Uncertainty)은 실용적인 범위를 결정하는 기준이 될 수 있다. 목표는 물리적으로 의미 없는 모델에서 생존하는 것이 아니라 현실적인 변화에 대한 강건성(Robustness)을 확보하는 것이다.

질량 및 관성 무작위화(Mass and Inertia Randomization)는 몸체와 개별 링크(Link)가 관절력과 지면 접촉에 반응하는 방식을 변화시킨다. 센서, 보호 커버, 장착 장비 또는 페이로드로 인해 베이스 질량이 달라질 수 있으며, 하드웨어 구성의 변화에 따라 무게중심 위치도 이동할 수 있다. 이러한 특성을 무작위화하면 정책이 액추에이터 출력, 몸체 가속도, 균형 응답 사이의 하나의 정확한 관계에 의존하는 것을 방지할 수 있다.

액추에이터 무작위화(Actuator Randomization)는 정책 명령이 실제 관절 동작으로 변환되는 과정의 불확실성을 표현한다. 모터 강도, PD 게인(PD Gain), 감쇠(Damping), 마찰, 토크 한계(Torque Limit), 액추에이터 네트워크 파라미터(Actuator-Network Parameter)를 독립적으로 또는 상관관계를 가진 모델을 통해 변화시킬 수 있다. 이를 통해 정책은 관절 응답이 조금씩 다른 로봇을 경험하게 되며, 불완전한 액추에이터 식별과 실제 플랫폼에 장착된 개별 모터 사이의 편차에 대한 민감도를 줄일 수 있다.

지면 상호작용(Ground Interaction)은 시뮬레이션-현실 오차의 또 다른 주요 원인이다. 마찰계수(Friction Coefficient), 반발계수(Restitution), 접촉 강성(Contact Stiffness), 감쇠, 국부적인 지형 특성을 무작위화하면 정책이 하나의 이상적인 접촉 모델만 가정하는 것을 방지할 수 있다. 특히 마찰 변화는 중요하다. 마찰이 부족하면 미끄러짐이 발생하고, 시뮬레이션에서 지나치게 높은 마찰을 사용하면 실제 하드웨어에서는 발생할 수 없는 수평력을 이용하여 보행이 실제보다 안정적으로 보일 수 있기 때문이다.

지형 무작위화(Terrain Randomization)는 지형 커리큘럼(Terrain Curriculum)을 보완한다. 커리큘럼 학습은 보행 문제가 얼마나 어려워질 것인지를 결정하고, 도메인 무작위화는 해당 난이도 내부에서 물리적 조건을 변화시킨다. 두 환경이 비슷한 수준의 거친 지형을 포함하더라도 서로 다른 마찰, 컴플라이언스(Compliance), 방향 또는 기하학적 교란(Geometric Perturbation)을 적용할 수 있다. 두 방법을 결합하면 모든 표면이 동일하게 동작한다고 가정하지 않으면서 점점 복잡해지는 지형에 대응하는 방법을 학습할 수 있다.

센서 무작위화(Sensor Randomization)는 정책이 비현실적으로 완벽한 관측값에 의존하는 것을 방지한다. 관성측정장치(IMU)의 각속도, 자세 추정값, 관절 위치, 관절 속도, 베이스 속도 추정값, 지형 측정값에 잡음(Noise), 바이어스(Bias), 스케일 오차(Scaling Error), 필터링 효과(Filtering Effect)를 적용할 수 있다. 이러한 교란의 크기와 시간적 특성은 실제 센싱 파이프라인(Sensing Pipeline)을 근사해야 하며, 독립적인 백색잡음(White Noise)만으로는 지속적인 바이어스나 상관된 측정 오차를 충분히 재현하지 못할 수 있다.

관측 지연(Observation Latency)과 행동 지연(Action Latency) 역시 무작위화할 수 있다. 하나의 고정 지연시간으로 학습하는 대신 측정된 타이밍 범위에서 버퍼 값을 선택하여 관측 데이터가 때때로 더 오래된 상태를 나타내고 명령이 액추에이터에 도달하는 시간도 달라지도록 할 수 있다. 특히 분산 소프트웨어 아키텍처(Distributed Software Architecture)에서는 스케줄링, 통신, 추론, 장치 처리 과정에서 평균 제어 주파수가 일정하더라도 가변적인 타이밍이 발생할 수 있으므로 지터(Jitter)를 고려하는 것이 중요하다.

외부 외란(External Disturbance)은 학습 과정에서 경험하는 동적 상태의 범위를 확장한다. 무작위 밀기(Random Push), 충격(Impulse), 베이스 속도 교란 또는 일시적인 외력은 충돌, 케이블에 의한 힘, 페이로드 움직임 또는 예상하지 못한 환경 상호작용을 표현할 수 있다. 외란의 크기, 방향, 지속시간, 발생 시점을 무작위화할 수 있다. 이러한 교란은 복구 행동(Recovery Behavior)을 유도하고 정책이 보행이 항상 외란이 없는 주기적인 보행 상태에서 진행된다고 가정하는 것을 방지한다.

명령 무작위화(Command Randomization)는 실제 운용에서 요구되는 움직임 범위(Operational Motion Envelope)를 포함해야 한다. 전진 속도, 횡방향 속도, 요 회전율(Yaw Rate), 정지 구간(Standing Period), 명령 전환(Command Transition)을 현실적인 한계 내에서 독립적으로 변화시킬 수 있다. 이를 통해 특정한 하나의 보행 속도가 아니라 다양한 행동에 대해 강건성을 학습할 수 있다. 특히 가속, 감속, 회전은 일정 속도 보행에서는 나타나지 않는 동적 약점을 드러낼 수 있으므로 명령 전환 구간도 학습 분포에 포함해야 한다.

무작위화는 각 파라미터의 물리적 의미에 따라 환경 초기화 시점(Environment Reset), 에피소드 중 일정한 시점 또는 지속적으로 적용할 수 있다. 로봇 질량이나 링크 관성은 일반적으로 하나의 에피소드 동안 일정하게 유지되는 반면 외부 외란은 언제든 변화할 수 있다. 센서 잡음은 지속적으로 변화하지만 페이로드는 임무 사이에서만 변경될 수 있다. 무작위화 시간 척도(Randomization Timescale)를 실제 현상과 일치시키면 시뮬레이터가 비현실적인 동역학을 생성하는 것을 방지할 수 있다.

독립적인 균등 샘플링(Independent Uniform Sampling)은 구현이 간단하지만 항상 물리적으로 적절한 것은 아니다. 일부 파라미터 사이에는 상관관계가 존재한다. 예를 들어 더 무거운 페이로드는 전체 질량뿐만 아니라 무게중심 위치도 변화시킬 수 있으며, 배터리 전압은 여러 관절의 가용 액추에이터 성능에 동시에 영향을 줄 수 있다. 구조화된 무작위화(Structured Randomization)를 사용하면 이러한 관계를 유지하면서도 넓은 불확실성 영역을 포함하는 물리적으로 타당한 가상 로봇을 생성할 수 있다.

무작위화 강도(Randomization Strength)는 점진적으로 증가시키는 것이 유용한 경우가 많다. 기본적인 보행 능력이 형성되기 전에 큰 파라미터 변화를 적용하면 최적화 문제가 불필요하게 어려워질 수 있다. 기준 동역학 근처에서 시작하여 정책 성능이 향상됨에 따라 범위를 점차 확대하는 무작위화 커리큘럼(Randomization Curriculum)을 적용할 수 있다. 이는 작업 커리큘럼(Task Curriculum)과 불확실성 커리큘럼(Uncertainty Curriculum)을 결합하며 처음부터 전체 불확실성 범위를 적용하는 것보다 안정적인 수렴을 제공할 수 있다.

과도한 무작위화는 부족한 무작위화만큼 문제가 될 수 있다. 학습 분포에 비현실적인 질량, 지연시간, 마찰값 또는 액추에이터 강도가 포함되면 정책은 지나치게 보수적으로 변하거나 실제로 발생하지 않을 조건에서 생존하기 위해 정상 조건의 성능을 희생할 수 있다. 반대로 무작위화 범위가 너무 좁으면 작은 하드웨어 불일치에도 정책이 취약해질 수 있다. 따라서 무작위화 분포는 일반적인 강건성 설정이 아니라 불확실성에 대한 공학적 모델(Engineering Model of Uncertainty)로 다루어야 한다.

특권 학습(Privileged Learning)은 학습 과정에서 무작위화된 파라미터를 활용할 수 있다. 교사(Teacher) 또는 특권 크리틱(Privileged Critic)은 실제로 샘플링된 질량, 마찰, 모터 강도, 지형 특성, 외란 상태를 입력받을 수 있지만 실제 배치되는 학생 정책(Student Policy)은 관측 가능한 움직임으로부터 그 영향을 추론해야 한다. 이를 통해 시뮬레이션의 정확한 정보를 효율적인 학습에 활용하면서도 실제 사족보행 로봇에서는 이러한 물리량을 직접 측정해야 하는 의존성을 제거할 수 있다.

무작위화의 효과는 평균 학습 반환값(Average Training Return)만으로 평가하지 않고 파라미터 스윕(Parameter Sweep)을 통해 검증해야 한다. 정책을 질량, 마찰, 지연시간, 액추에이터 강도, 센서 잡음, 지형 조건에 걸쳐 체계적으로 시험하여 실패 경계(Failure Boundary)를 확인할 수 있다. 이러한 강건성 지도(Robustness Map)는 정책이 넓고 안정적인 영역을 학습했는지 또는 단순히 학습 분포의 중심 부근에서만 높은 성능을 나타내는지를 보여준다.

절제 실험(Ablation Study)은 어떤 불확실성 요인이 가장 중요한지 확인하는 데 유용하다. 마찰 무작위화, 액추에이터 변화, 지연시간 변화, 센서 잡음 또는 외부 외란을 각각 제거한 별도의 정책을 학습하고 동일한 평가 조건에서 비교할 수 있다. 이를 통해 불필요한 복잡성을 줄이고 어떤 파라미터의 불일치가 보행 전이에 가장 큰 영향을 미치는지 확인하여 시뮬레이션 모델링 노력을 물리적으로 중요한 불확실성에 집중할 수 있다.

하드웨어 측정값(Hardware Measurement)은 무작위화 분포를 지속적으로 개선하는 데 사용해야 한다. 관절 응답 로그, 타이밍 측정값, 전류 및 토크 추정값, IMU 통계, 접촉 동작, 페이로드 구성, 필드 시험 실패 사례를 분석하면 최초에 설정한 파라미터 범위가 현실적인지를 확인할 수 있다. 따라서 시뮬레이션-현실 전이 개발은 반복적인 과정이 되며, 실제 하드웨어 데이터가 시뮬레이션 분포를 개선하고 수정된 시뮬레이션은 이후 하드웨어 시험에 더욱 잘 준비된 정책을 생성한다.

가장 강건한 정책은 반드시 가장 높은 시뮬레이션 보상을 얻는 정책이 아니라 물리 파라미터가 기준값에서 벗어날 때 성능이 점진적으로 저하되는 정책이다. 따라서 명령 추종(Command Tracking), 전도율(Fall Rate), 에너지 소비, 발 미끄러짐(Foot Slip), 토크 포화(Torque Saturation), 복구 성공률(Recovery Success), 지형 통과 성능(Terrain Completion)을 무작위화된 평가 공간 전체에서 측정해야 한다. 강건성은 학습 통계로부터 추정하는 것이 아니라 폐루프 보행(Closed-Loop Locomotion)의 실제 특성으로 입증되어야 한다.

사족보행 강화학습(Quadruped Reinforcement Learning)의 전체 흐름에서 도메인 무작위화는 지형 변화, 특권 학습, 액추에이터 모델링(Actuator Modeling), 타이밍 불확실성(Timing Uncertainty), 센싱 불완전성(Sensing Imperfection), 동적 외란(Dynamic Disturbance)을 하나의 통합된 시뮬레이션-현실 전이 학습 분포(Sim2Real Training Distribution)로 결합한다. 이를 통해 학습된 정책이 시뮬레이터 고유의 가정에 의존하는 것을 줄여 제로샷 전이(Zero-Shot Transfer)를 준비하며, 이후 단계에서는 이러한 강건성이 온보드 추론(Onboard Inference)과 실제 제품 배치(Production Deployment)에서도 유지되는지를 검증하게 된다.

## 07.08. Zero Shot Sim2Real Transfer ANYmal Case [w/Code]

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

제로샷 시뮬레이션-현실 전이(Zero-Shot Sim2Real Transfer)는 실제 환경의 보행 데이터를 이용한 추가적인 정책 최적화(Policy Optimization) 없이, 전적으로 시뮬레이션에서 학습된 보행 정책(Locomotion Policy)을 실제 사족보행 로봇(Physical Quadruped)에 배치하는 것을 의미한다. ANYmal 유형의 사례에서 성공 여부는 하나의 전이 기법에 의해서 결정되는 것이 아니라, 하드웨어 배치 이전에 구축된 시뮬레이션 정확도와 강건성(Robustness), 액추에이터 모델링(Actuator Modeling), 관측 설계(Observation Design), 보상 공학(Reward Engineering), 지형 커리큘럼(Terrain Curriculum), 도메인 무작위화(Domain Randomization)의 종합적인 완성도에 의해 결정된다.

핵심적인 과제는 시뮬레이션 동역학과 실제 물리 동역학 사이에 존재하는 현실 격차(Reality Gap)이다. 높은 충실도의 강체 시뮬레이션(High-Fidelity Rigid-Body Simulation)도 관절 마찰, 액추에이터 응답, 구조적 컴플라이언스(Structural Compliance), 발-지면 접촉(Foot-Ground Contact), 센서 잡음, 배터리 영향, 페이로드 관성(Payload Inertia), 환경 외란(Environmental Disturbance)의 모든 특성을 완벽하게 재현할 수는 없다. 작은 차이도 폐루프 제어(Closed-Loop Control)를 통해 누적될 수 있으며, 학습된 정책이 실제 로봇에서 실행될 때 상당히 다른 보행 동작을 발생시킬 수 있다.

ANYmal급 사족보행 로봇(ANYmal-Class Quadruped)은 여러 관절의 연속적인 상호작용, 몸체 관성(Body Inertia), 지면 반력(Ground Reaction Force), 마찰, 접촉 타이밍(Contact Timing), 액추에이터 동역학을 통해 안정적인 보행이 형성되기 때문에 매우 까다로운 전이 문제를 제시한다. 각각의 발 착지(Foot Placement)는 전신에 작용하는 힘의 분포를 변화시킨다. 따라서 성공적인 전이를 위해서는 하나의 정확한 물리 모델에 의존하는 궤적을 기억하는 것이 아니라 다양한 조건에서도 동작할 수 있는 강건한 폐루프 행동(Robust Closed-Loop Behavior)을 시뮬레이션에서 학습해야 한다.

시뮬레이션 모델은 먼저 로봇의 주요 물리적 특성을 충분한 정확도로 재현해야 한다. 링크 질량(Link Mass), 관성, 관절 한계(Joint Limit), 발 형상(Foot Geometry), 충돌 형상(Collision Shape), 액추에이터 성능, 제어 주파수(Control Frequency)를 이용하여 기준 모델(Nominal Model)을 구성한다. 이후 시스템 식별(System Identification)을 통해 관절 마찰, 액추에이터 동역학, 센서 지연시간(Sensor Latency), 배터리 상태에 따른 동작, 페이로드 관성, 접촉 역학(Contact Mechanics), 구조적 유연성(Structural Flexibility)과 같이 불확실한 요소를 개선한 후 최종 정책 학습을 수행한다.

액추에이터 모델링은 학습된 정책이 관절 수준의 동역학을 통해 환경과 상호작용하기 때문에 특히 중요하다. 이상적인 토크 소스(Ideal Torque Source) 또는 완벽하게 반응하는 위치 서보(Position Servo)는 실제 모터에서 재현할 수 없는 행동을 허용할 수 있다. 현실적인 모델에서는 제한된 액추에이터 출력, 추종 동역학(Tracking Dynamics), 감쇠(Damping), 마찰, 포화(Saturation), 지연시간을 표현하여 시뮬레이션에서 생성된 행동이 실제 물리 플랫폼에서 구현 가능한 응답과 충분히 유사하도록 해야 한다.

접촉 모델링(Contact Modeling)은 또 다른 중요한 전이 경계를 형성한다. 보행은 지속적으로 지면 반력, 마찰, 충격(Impact), 미끄러짐(Slip), 컴플라이언스, 지형 변형(Terrain Deformation)의 영향을 받는다. 이상적인 강체 지면에서만 학습한 정책은 실제 표면에서는 존재하지 않는 접촉 특성을 이용할 수 있다. 따라서 학습 과정에서는 하나의 완벽하게 알려진 발-지면 상호작용만 가정하지 않고 다양한 마찰, 컴플라이언스, 거칠기(Roughness), 안정성을 정책에 경험시켜야 한다.

시뮬레이션에서 사용하는 관측 인터페이스(Observation Interface)는 실제 로봇에서 사용할 수 있는 정보와 대응되어야 한다. 관절 위치, 관절 속도, 관성 측정값(Inertial Measurement), 몸체 움직임 추정값(Body Motion Estimate), 접촉 관련 신호, 지형 정보, 명령된 움직임(Commanded Motion)을 이용하여 보행 상태를 표현할 수 있다. 물리적으로 의미 있는 압축된 표현(Compact Representation)을 사용하면 균형, 명령 추종, 지형 적응에 필요한 정보를 유지하면서 시뮬레이터에만 존재하는 상태 정보에 대한 불필요한 의존성을 줄일 수 있다.

행동 인터페이스(Action Interface) 역시 실제 배치 환경과 호환되어야 한다. 강화학습 정책이 비현실적인 직접 액추에이터 인터페이스에 의존하도록 하는 대신 계층형 아키텍처(Hierarchical Architecture)를 사용하여 관절 위치 목표(Joint Position Target), 보행 관련 명령 또는 기타 기준값을 생성하고 결정론적 하위 제어기(Deterministic Low-Level Controller)가 이를 실행하도록 할 수 있다. 이러한 분리는 학습 기반 적응성을 유지하면서 빠른 모터 제어와 하드웨어 보호 기능을 기존 제어 루프(Control Loop) 내부에 유지할 수 있게 한다.

보상 공학(Reward Engineering)은 정책이 물리적으로 바람직하지 않은 행동으로 속도 추종을 달성하는 것을 억제함으로써 실제 전이를 준비한다. 안정성, 에너지 소비, 발 미끄러짐(Foot Slip), 과도한 관절 움직임, 급격한 가속, 불필요한 진동을 모두 학습 행동에 반영할 수 있다. 부드럽고 효율적인 보행은 액추에이터의 부하를 줄이는 동시에 검사용 사족보행 로봇이 탑재하는 지각 센서(Perception Payload)를 위해 보다 안정적인 몸체 움직임을 제공한다.

지형 커리큘럼 학습(Terrain Curriculum Learning)은 보행 정책이 경험하는 분포를 점진적으로 확대한다. 초기 학습에서는 단순한 지면에서 안정적인 보행을 확립한 후 거친 지형, 경사면, 계단, 암석, 외란, 페이로드 변화, 액추에이터 지연, 센서 불확실성을 점진적으로 도입할 수 있다. 이러한 단계적 학습 과정은 전이와 관련된 어려운 조건이 초기 최적화를 방해하지 않도록 하면서 최종적으로 일반적인 실험실 바닥보다 훨씬 광범위한 조건에서 정책이 동작하도록 만든다.

도메인 무작위화(Domain Randomization)는 남아 있는 모델 불확실성을 학습 분포(Training Distribution)로 변환한다. 지면 마찰, 액추에이터 특성, 페이로드 질량, 관절 감쇠, 센서 보정(Sensor Calibration), 지형 형상, 접촉 컴플라이언스, 통신 지연(Communication Latency), 기계적 공차(Mechanical Tolerance)를 시뮬레이션 에피소드마다 변화시킬 수 있다. 따라서 정책은 하나의 정확한 로봇이나 환경에 의존할 수 없으며, 현실적으로 발생할 수 있는 물리적 변화 전반에서 유효한 보행 전략을 학습해야 한다.

외부 외란 주입(External Disturbance Injection)은 학습 과정에서 경험하는 상태 분포를 더욱 확장한다. 무작위 외력(Random Force)과 충격은 예상하지 못한 접촉, 불균일한 하중, 환경에서 발생하는 힘 또는 국부적인 지형 붕괴를 표현할 수 있다. 정책은 안정된 주기적 보행 상태만 경험하는 것이 아니라 반복적으로 상태 편차를 경험하고, 작업을 계속 수행하면서 균형을 회복해야 한다. 이를 통해 실제 하드웨어에 정책을 적용하기 전에 복구 동작(Recovery Behavior)이 폐루프 행동의 일부로 학습된다.

제로샷 전이는 학습 과정에서 하드웨어에 대한 지식이 전혀 사용되지 않는다는 의미가 아니다. 오히려 실제 플랫폼에서 측정한 값은 기준 시뮬레이션 파라미터와 현실적인 무작위화 범위를 결정하는 데 사용되어야 한다. 제로샷이라는 용어는 최종 정책이 최초 실제 배치 이전에 실제 보행 시험으로부터 얻은 데이터를 사용하여 추가적인 강화학습 업데이트(Reinforcement-Learning Update)를 수행할 필요가 없다는 것을 의미한다. 따라서 정책 최적화는 시뮬레이션에서 수행되지만 하드웨어 특성화(Hardware Characterization)는 전이 이전에 이루어진다.

최초의 하드웨어 실행(Hardware Execution)은 보수적인 운용 조건에서 수행해야 한다. 명령 속도, 지형 난이도, 외란 노출, 동작 지속시간을 제한하면서 엔지니어는 실제 응답과 시뮬레이션 결과를 비교할 수 있다. 관절 추종(Joint Tracking), 몸체 자세(Body Orientation), 접촉 타이밍, 발 궤적(Foot Trajectory), 액추에이터 부하(Actuator Loading), 에너지 동작을 분석하면 학습된 제어기가 학습 과정에서 표현된 동역학 영역 내부에서 유지되는지를 판단할 수 있다.

실제 배치는 제한되지 않은 현장 환경에 즉시 적용하기보다 통제된 시험 환경(Controlled Test Environment)에서 시작해야 한다. 실험실 바닥, 인공 지형(Artificial Terrain), 램프(Ramp), 계단, 자갈, 장애물 코스를 이용하여 점진적으로 더 어려운 조건을 검증할 수 있다. 이후 보행 안정성, 복구 능력, 에너지 소비, 발 궤적, 액추에이터 부하, 몸체 움직임을 예상된 시뮬레이션 동작과 비교한 후 실제 운용 범위(Operational Envelope)를 단계적으로 확대할 수 있다.

성공적인 제로샷 정책(Zero-Shot Policy)은 마찰, 페이로드, 모터 응답, 타이밍, 지형의 차이를 허용하면서도 명령 추종 성능을 유지해야 한다. 실제 시스템은 필연적으로 시뮬레이션과 차이가 있으므로 시뮬레이션에서 생성된 궤적을 실제 로봇이 정확하게 재현하는 것은 필요하지도 바람직하지도 않다. 더 중요한 기준은 폐루프 보행이 안정적으로 유지되는지, 그리고 실제 동역학이 기준 시뮬레이션 조건에서 벗어날 때 성능이 급격하게 붕괴하지 않고 점진적으로 저하되는지 여부이다.

실패 분석(Failure Analysis)에서는 정책 자체의 한계와 시뮬레이션 모델의 오차를 구분해야 한다. 반복적인 발 미끄러짐은 비현실적인 마찰 분포를 의미할 수 있고, 늦은 복구 반응은 타이밍 불일치(Timing Mismatch)를 나타낼 수 있으며, 체계적인 관절 추종 오차는 액추에이터 모델의 결함을 드러낼 수 있다. 따라서 장기적인 목표가 광범위한 실제 환경 강화학습이 아니라 제로샷 전이라 하더라도 하드웨어 관측 결과를 이용하여 시스템 식별과 무작위화 범위를 지속적으로 개선할 수 있다.

성공적인 전이 이후에도 런타임 안전 감독(Runtime Safety Supervision)은 필요하다. 독립적인 안전 메커니즘(Safety Mechanism)은 몸체 자세, 관절 한계, 액추에이터 온도, 배터리 상태, 통신 상태, 센서 무결성(Sensor Integrity), 충돌 위험을 지속적으로 모니터링할 수 있다. 따라서 학습 기반 보행은 사전에 정의된 하드웨어 제약이 위반될 경우 명령을 수정하거나 무효화할 수 있는 보다 광범위한 안전 아키텍처(Safety Architecture) 내부에서 동작해야 한다.

평가는 단순히 보행 동작이 시각적으로 자연스러운지를 확인하는 수준을 넘어야 한다. 명령 추종 오차(Command-Tracking Error), 전도 빈도(Fall Frequency), 복구 성공률(Recovery Success), 발 미끄러짐, 에너지 소비, 액추에이터 포화(Actuator Saturation), 몸체 진동(Body Oscillation), 지형 통과 성능(Terrain Completion)은 전이 품질을 정량적으로 평가할 수 있는 지표이다. 하나의 실험실 바닥에서 성공적으로 보행하는 것만으로는 목표로 하는 실제 배치 분포 전체에서의 강건성을 입증할 수 없으므로 다양한 표면과 페이로드 조건에서 시험해야 한다.

ANYmal 유형의 산업용 배치(Industrial Deployment)에서 보행 정책은 궁극적으로 상위 수준의 검사 및 자율 기능(Autonomy Function)을 지원한다. 실제 임무에는 불규칙한 지형, 계단, 자갈, 변화하는 환경 조건, 온보드 센싱 페이로드(Onboard Sensing Payload)가 포함될 수 있다. 따라서 안정적인 보행은 독립적인 시연 기능이 아니라 지각(Perception)과 임무 수행(Mission Execution)을 지원하는 기반 인프라가 되며, 시뮬레이션-현실 전이 강건성(Sim2Real Robustness)은 전체 피지컬 AI 시스템(Physical AI System)의 신뢰성에 직접적인 영향을 미친다.

결과적으로 제로샷 시뮬레이션-현실 전이는 앞선 강화학습 파이프라인(Reinforcement-Learning Pipeline)을 통합적으로 검증하는 단계이다. PPO는 최적화 메커니즘을 제공하고, 보상 공학은 유용한 행동을 정의하며, 지형 커리큘럼은 보행 능력을 확장한다. 특권 학습(Privileged Learning)은 시뮬레이션 정보를 활용하고, 액추에이터 및 지연 모델(Actuator and Delay Model)은 동적 충실도(Dynamic Fidelity)를 향상시키며, 도메인 무작위화는 강건성을 구축한다. 이러한 요소들의 결합을 통해 실제 환경에서 추가적인 정책 재학습 없이 시뮬레이션에서 실제 사족보행 로봇 하드웨어로 전이할 수 있는 정책을 준비할 수 있다.

## 07.09. RL Policy Onboard Inference 50Hz Jetson [w/Code]

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

온보드 추론(Onboard Inference)은 시뮬레이션에서 학습된 강화학습 기반 보행 정책(Reinforcement-Learning Locomotion Policy)을 사족보행 로봇에서 직접 실행되는 결정론적 실시간 제어 구성 요소(Deterministic Real-Time Control Component)로 변환하는 과정이다. 50 Hz 정책 루프(Policy Loop)는 20 ms마다 새로운 행동(Action)을 생성하므로, 센싱(Sensing), 상태 추정(State Estimation), 관측값 구성(Observation Construction), 신경망 추론(Neural-Network Inference), 안전 처리(Safety Processing), 명령 발행(Command Publication)이 Jetson급 임베디드 컴퓨터(Embedded Computer)의 예측 가능한 타이밍 예산(Timing Budget) 내에서 완료되어야 한다.

50 Hz의 정책 주파수(Policy Frequency)는 더 높은 주파수로 동작하는 하위 모터 제어 루프(Low-Level Motor-Control Loop)와 구분해야 한다. 강화학습 정책은 20 ms마다 목표 관절 위치(Desired Joint Position), 잔차 명령(Residual Command) 또는 기타 기준값을 생성할 수 있으며, 임베디드 관절 제어기(Embedded Joint Controller)는 수백 Hz에서 수 kHz의 주파수로 PD 제어(PD Control) 또는 임피던스 제어(Impedance Control)를 실행한다. 이러한 다중 주기 아키텍처(Multirate Architecture)를 통해 학습된 전신 동작과 빠르고 결정론적인 액추에이터 제어를 함께 사용할 수 있다.

각 추론 주기(Inference Cycle)는 학습된 정책이 요구하는 관측값(Observation)을 획득하는 과정에서 시작된다. 일반적인 입력에는 관절 위치, 관절 속도, 몸체 각속도(Body Angular Velocity), 투영 중력(Projected Gravity), 명령된 선형 속도 및 요 속도(Yaw Velocity), 이전 행동(Previous Action), 그리고 필요한 경우 관측 이력(Observation History)이나 지형 특징(Terrain Feature)이 포함된다. 실제 배치에서 사용하는 관측 벡터는 시뮬레이션 학습에서 사용한 순서, 단위, 좌표계 규칙, 스케일링(Scaling), 클리핑(Clipping), 정규화(Normalization)를 정확하게 유지해야 한다.

상태 추정 타이밍(State-Estimation Timing)은 신경망 실행 시간만큼 중요하다. 관절 인코더(Joint Encoder)와 관성측정장치(IMU)의 측정값은 서로 다른 주기와 타임스탬프(Timestamp)로 도착할 수 있으며, 속도 또는 자세 추정에는 필터링(Filtering)과 센서 융합(Sensor Fusion)이 필요하다. 따라서 추론 파이프라인(Inference Pipeline)은 단순히 가장 최근의 값을 결합하는 것이 아니라 일관된 제어 타임스탬프(Control Timestamp)를 기준으로 관측값을 구성해야 한다. 그렇지 않으면 서로 다른 실제 시점의 물리 상태가 하나의 관측값에 혼합될 수 있다.

관측 정규화(Observation Normalization)는 학습 설정에서 사용한 구성을 그대로 실제 배치 환경으로 이전해야 한다. 각속도, 관절 변위(Joint Displacement), 관절 속도, 명령, 지형 측정값, 관측 이력에 적용되는 스케일링 계수(Scaling Factor)는 신경망이 입력으로 받는 수치 분포를 결정한다. 실제 물리량이 정확하더라도 정규화 방식이 일치하지 않으면 추론 입력이 학습 과정에서 경험한 분포에서 크게 벗어나 불안정하거나 이해하기 어려운 행동을 생성할 수 있다.

신경망 정책(Neural Policy) 자체는 일반적으로 대규모 지각 모델(Perception Model)에 비해 비교적 작다. 다층 퍼셉트론(Multilayer Perceptron)은 소수의 완전연결 계층(Fully Connected Layer)과 비선형 활성화 함수(Nonlinear Activation)를 이용하여 정규화된 보행 관측값을 행동으로 변환할 수 있다. 이력 의존형 정책(History-Dependent Policy)에서는 추가적인 시간 인코더(Temporal Encoder) 또는 순환 구성 요소(Recurrent Component)를 사용할 수 있다. 실제 배치에서는 행동 생성에 필요한 학생 측(Student-Side) 또는 액터 측(Actor-Side) 연산만 유지하고 학습 전용 크리틱(Critic)과 특권 입력(Privileged Input)은 제외해야 한다.

Jetson 플랫폼은 정책 네트워크와 주변 소프트웨어가 사용 가능한 연산 자원, 메모리, 전력, 열적 한계(Thermal Envelope) 내에 들어갈 경우 적합한 온보드 플랫폼이 될 수 있다. GPU 가속(GPU Acceleration)은 추론 시간을 줄일 수 있지만 단순한 처리량(Throughput)만으로 적합성을 판단해서는 안 된다. 보행 제어에서는 낮은 지연시간과 낮은 지터(Jitter)가 중요하므로 평균 신경망 처리량뿐만 아니라 최악 실행시간(Worst-Case Execution Time)과 타이밍 분포(Timing Distribution)를 기준으로 배치 구성을 평가해야 한다.

추론 모델은 학습 프레임워크(Training Framework)에서 ONNX와 같은 배치 표현(Deployment Representation)으로 내보낸 후 최적화된 런타임(Optimized Runtime)을 통해 실행할 수 있다. NVIDIA Jetson 플랫폼에서는 TensorRT를 사용하여 지원되는 신경망 연산을 최적화하고 실행 오버헤드(Execution Overhead)를 줄일 수 있다. 내보낸 모델은 실제 하드웨어를 제어하기 전에 원래의 학습 구현과 비교하여 수치적으로 검증(Numerical Validation)해야 한다.

수치 검증에서는 동일한 관측 벡터를 원래 정책과 실제 배치용 추론 엔진(Inference Engine)에 각각 입력한 후 출력값을 비교해야 한다. 작은 부동소수점 차이(Floating-Point Difference)는 허용할 수 있지만 체계적인 편차는 지원되지 않는 연산자(Unsupported Operator), 모델 변환 오류(Export Error), 활성화 함수 차이, 정규화 오류 또는 정밀도 관련 문제를 의미할 수 있다. 이러한 오프라인 동등성 시험(Offline Equivalence Test)을 통해 소프트웨어 변환 오류가 실제 보행 실패로 이어지기 전에 분리하여 확인할 수 있다.

FP32 추론은 일반적으로 학습 과정에서 사용된 수치 동작과 유사하므로 유용한 기준 구현(Reference Implementation)을 제공한다. FP16은 호환되는 Jetson 하드웨어에서 메모리 대역폭을 줄이고 추론 성능을 향상시킬 수 있지만, 대표적인 관측 분포에 대해 정책을 다시 검증해야 한다. INT8 최적화(INT8 Optimization)는 양자화 오차(Quantization Error)가 폐루프 접촉 동역학(Closed-Loop Contact Dynamics)에 영향을 미치는 작은 행동 차이를 변화시킬 수 있으므로 더욱 신중하게 적용해야 한다.

20 ms 제어 주기(Control Cycle)를 구현하려면 명확한 타이밍 할당(Timing Allocation)이 필요하다. 센서 동기화(Sensor Synchronization)와 상태 추정이 주기의 일부를 사용하고, 관측 전처리(Observation Preprocessing)가 추가 시간을 소비하며, 신경망 추론은 제한된 실행시간 내에서 완료되어야 한다. 이후 안전 검사와 명령 전송까지 데드라인(Deadline) 이전에 완료되어야 한다. 운영체제 스케줄링이나 장치 활동이 일시적으로 증가하더라도 즉시 제어 업데이트 실패로 이어지지 않도록 충분한 공학적 여유(Engineering Margin)를 확보해야 한다.

지연시간(Latency)은 신경망 호출 구간만 측정하는 것이 아니라 종단간(End-to-End)으로 측정해야 한다. 실제로 중요한 지연시간은 센서 샘플링에서 시작하여 상태 추정, 정책 실행, 명령 전송, 하위 제어 처리, 최종 액추에이터 응답까지 이어진다. 정책 자체의 추론 시간이 1 ms보다 훨씬 짧더라도 상위 단계의 관측 데이터가 오래되었거나 하위 단계의 명령이 모터에 도달하기 전에 버퍼에 머물면 실제 유효 지연(Effective Delay)은 상당히 커질 수 있다.

지터는 강화학습 정책이 일반적으로 정의된 제어 시간 간격(Control Interval)을 기준으로 학습되기 때문에 특히 위험하다. 하나의 행동이 20 ms 동안 적용된 후 다음 행동이 예상보다 훨씬 오랫동안 유지되면 실제 제어기 동역학이 달라진다. 타임스탬프 모니터링(Timestamp Monitoring), 데드라인 통계(Deadline Statistics), 제한된 큐(Bounded Queue), 적절한 프로세스 우선순위(Process Priority), 통제된 통신 경로를 사용하면 실제 온보드 연산 부하에서도 예측 가능한 동작을 유지하는 데 도움이 된다.

행동 후처리(Action Postprocessing)는 학습 과정에서 사용한 인터페이스를 정확하게 재현해야 한다. 신경망 출력은 직접적인 물리 명령이 아니라 정규화된 관절 오프셋(Normalized Joint Offset)을 의미할 수 있으므로 스케일링, 기준 관절 구성(Nominal Joint Configuration)의 추가, 액추에이터 기준값으로의 변환 과정이 필요할 수 있다. 행동 클리핑(Action Clipping)은 학습에서 사용한 한계와 일치해야 하며, 독립적인 하드웨어 안전 계층(Hardware Safety Layer)은 필요한 경우 더 엄격한 절대 관절, 속도, 토크 또는 작업공간 제한(Workspace Constraint)을 적용할 수 있다.

이전 행동 입력(Previous-Action Input)은 추론 인터페이스 내부에 시간적 상태(Temporal State)를 형성하므로 세심한 구현이 필요하다. 다음 주기에 입력되는 값은 다른 소프트웨어 계층에서 임의로 수정된 모터 명령이 아니라 학습에서 정의한 행동과 동일한 의미를 가져야 한다. 마찬가지로 누적 관측 이력(Stacked Observation History)을 사용하는 정책에서는 결정론적인 버퍼 초기화(Buffer Initialization), 업데이트 순서, 리셋 동작을 유지하여 실제 배치에서 시뮬레이션 학습과 다른 시간적 시퀀스가 입력되는 것을 방지해야 한다.

온보드 소프트웨어 아키텍처(Onboard Software Architecture)는 하드 실시간(Hard Real-Time) 또는 안전 중요 기능(Safety-Critical Function)을 계산 시간이 변동될 수 있는 작업과 분리해야 한다. 지각(Perception), 매핑(Mapping), 로깅(Logging), 시각화(Visualization), 통신 기능이 보행 추론과 동일한 Jetson을 사용할 수 있지만 정책 루프를 예측할 수 없게 차단해서는 안 된다. 자원 격리(Resource Isolation), 제한된 메시지 큐(Bounded Message Queue), 프로세스 우선순위, 제어된 GPU 사용을 통해 보행과 상위 수준 자율 기능 사이의 간섭을 줄일 수 있다.

열 및 전력 동작(Thermal and Power Behavior)도 시험해야 한다. 지속적인 임베디드 추론은 짧은 시간 동안 수행하는 벤치마크 실행과 다르기 때문이다. Jetson의 클록 주파수(Clock Frequency)는 전력 모드(Power Mode)나 열 관리(Thermal Management)에 따라 변경될 수 있으며, 장시간 동작한 이후 추론 지연시간이 달라질 수 있다. 따라서 실제 배치에서 예상되는 지각 및 자율 기능 부하를 함께 실행한 장시간 시험을 수행하여 예상되는 전력과 온도 조건에서도 50 Hz 보행 데드라인을 계속 만족하는지 확인해야 한다.

실제 로봇 시험 전에 실패 처리(Failure Handling) 방법을 정의해야 한다. 관측값 누락(Missing Observation), 오래된 타임스탬프(Stale Timestamp), 추론 예외(Inference Exception), NaN 값, 과도한 행동 크기, 통신 손실, 반복적인 데드라인 미준수는 결정론적인 대응을 발생시켜야 한다. 로봇 아키텍처에 따라 안전 명령 유지, 안정 자세(Stable Posture)로의 전환, 명령 속도 감소, 대체 제어기(Fallback Controller)로의 제어권 전환 또는 비상 정지(Emergency Stop)를 수행할 수 있다.

전체 파이프라인을 검증하려면 계측(Instrumentation)이 필요하다. 각 제어 주기마다 관측 타임스탬프, 전처리 시간, 추론 지연시간, 행동값, 명령 발행 시간, 데드라인 상태, 선택된 로봇 상태 변수를 기록할 수 있다. 이러한 로그를 이용하면 모든 하드웨어 문제를 강화학습 자체의 문제로 판단하는 대신 보행 불안정성과 타이밍 오류, 센서 이상(Sensor Anomaly), 행동 포화(Action Saturation), 모델 동작 사이의 상관관계를 분석할 수 있다.

하드웨어 인 더 루프 시험(Hardware-in-the-Loop Testing)은 제한되지 않은 실제 보행 이전의 중간 검증 단계로 활용할 수 있다. 실제 배치용 Jetson 추론 스택(Inference Stack)을 목표 주파수인 50 Hz로 실행하면서 시뮬레이션, 기록된 관측값 또는 제한된 물리 시험 환경과 상호작용하도록 할 수 있다. 이를 통해 실제 사족보행 로봇에 적용할 것과 동일한 소프트웨어 경로를 사용하여 모델 로딩, 타이밍, 관측 구성, 통신, 리셋 처리, 안전 감독(Safety Supervision)을 검증할 수 있다.

초기 보행 시험(Initial Walking Test)은 보수적인 명령과 통제된 지형에서 시작하고 타이밍과 정책 출력을 지속적으로 모니터링해야 한다. 안정적인 동작이 확인되면 속도 범위, 회전 명령, 지형 난이도, 페이로드 변화, 외란 노출을 단계적으로 확대할 수 있다. 이러한 과정의 목적은 실제 로봇에서 정책을 다시 학습시키는 것이 아니라 실제 배치된 추론 구현이 시뮬레이션-현실 전이(Sim2Real) 학습 과정에서 확보한 강건한 동작을 그대로 유지하는지 검증하는 것이다.

따라서 성공적인 50 Hz Jetson 배치는 단순히 신경망을 임베디드 GPU에 탑재하는 것 이상의 작업을 요구한다. 전체 제어 경로는 학습 단계에서 정의된 관측 및 행동 계약(Observation and Action Contract)을 유지하면서 결정론적 타이밍(Deterministic Timing), 수치적 동등성(Numerical Equivalence), 연산 자원 격리(Computational Isolation), 열적 안정성(Thermal Stability), 런타임 안전성(Runtime Safety) 요구조건을 충족해야 한다. 결과적으로 온보드 추론은 제로샷 시뮬레이션-현실 전이(Zero-Shot Sim2Real Transfer)와 실제 운용 환경에서의 지속적인 사족보행 로봇 동작을 연결하는 실행 계층(Execution Bridge)의 역할을 한다.

## 07.10. RL Locomotion Policy Production Deployment [w/Code]

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

강화학습 기반 보행 정책(Reinforcement-Learning Locomotion Policy)의 제품 배치(Production Deployment)는 성공적인 연구용 제어기(Research Controller)를 실제 임무 조건에서 반복적으로 운용할 수 있는 유지보수 가능한 로봇 소프트웨어 구성 요소(Robotic Software Component)로 전환하는 과정이다. 목표는 더 이상 단순히 안정적인 보행을 시연하는 것에 머물지 않는다. 실제 배치된 정책은 신뢰성(Reliability), 결정론적 실행(Deterministic Execution), 안전성(Safety), 하드웨어 호환성(Hardware Compatibility), 진단(Diagnostics), 구성 관리(Configuration Control), 복구(Recovery), 장시간 운용(Long-Duration Operation)에 대한 요구사항을 충족해야 한다.

제품용 정책(Production Policy)은 독립적인 신경망 체크포인트(Neural-Network Checkpoint)가 아니라 버전이 관리되는 소프트웨어 및 모델 산출물(Versioned Software and Model Artifact)로 취급해야 한다. 배치 패키지(Deployment Package)에는 네트워크 가중치(Network Weights), 관측 정의(Observation Definition), 정규화 파라미터(Normalization Parameter), 행동 스케일링(Action Scaling), 제어 주파수(Control Frequency), 관절 구성(Joint Configuration), 액추에이터 가정(Actuator Assumption), 학습 구성(Training Configuration), 호환 가능한 로봇 하드웨어를 명확하게 정의해야 한다. 이를 통해 외형상 동일한 모델이 호환되지 않는 런타임 설정(Runtime Setting)에서 실행되는 문제를 방지할 수 있다.

엄격한 관측 계약(Observation Contract)은 필수적이다. 신경망 정책은 학습 과정에서 사용한 입력 표현(Input Representation)을 정확하게 전제로 하기 때문이다. 관절 위치, 관절 속도, 관성측정장치(IMU) 신호, 투영 중력(Projected Gravity), 명령된 움직임(Commanded Motion), 이전 행동(Previous Action), 지형 특징(Terrain Feature), 관측 이력(Observation History)은 정의된 순서, 단위, 기준 좌표계(Reference Frame), 스케일링(Scaling), 클리핑(Clipping), 타이밍을 그대로 유지해야 한다. 하나의 전처리 구성 요소만 변경되어도 신경망 가중치가 동일한 상태에서 정책 동작이 달라질 수 있다.

행동 계약(Action Contract)에도 동일한 수준의 엄격한 관리가 필요하다. 정책 출력은 직접적인 액추에이터 명령이 아니라 정규화된 관절 오프셋(Normalized Joint Offset), 목표 위치(Desired Position), 잔차 행동(Residual Action) 또는 기타 기준값을 의미할 수 있다. 제품 소프트웨어는 학습 과정에서 사용한 것과 동일한 스케일링, 기준 자세(Nominal Posture), 클리핑, 변환(Transformation)을 적용해야 한다. 이후 학습된 행동 인터페이스(Action Interface)의 의미를 변경하지 않으면서 하드웨어별 안전 제약(Hardware-Specific Safety Constraint)을 독립적으로 적용할 수 있다.

보행 정책은 계층형 제어 아키텍처(Hierarchical Control Architecture) 내부에서 동작해야 한다. 학습된 제어기는 설계된 정책 주파수에서 적응형 전신 명령(Adaptive Whole-Body Command)을 생성하고, 더 빠른 결정론적 관절 제어기(Deterministic Joint Controller)는 토크, 위치 또는 임피던스(Impedance)를 제어할 수 있다. 상위 수준의 내비게이션(Navigation)은 속도 및 회전 명령을 제공하며, 독립적인 안전 메커니즘(Safety Mechanism)은 전체 시스템을 감독한다. 이러한 분리는 신경망 정책의 책임 범위를 제한하고 검증 과정을 단순화한다.

런타임 타이밍(Runtime Timing)은 실제 연산 부하에서도 결정론적으로 유지되어야 한다. 지각(Perception), 매핑(Mapping), 내비게이션, 통신, 로깅(Logging), 사용자 인터페이스(User Interface)가 보행 기능과 동시에 실행될 수 있지만 허용할 수 없는 추론 지연(Inference Delay)이나 지터(Jitter)를 발생시켜서는 안 된다. 제품 검증에서는 예상되는 모든 온보드 작업이 실행되는 상태에서 전체 제어 주기 지연시간(Control-Cycle Latency), 데드라인 미준수(Deadline Miss), 관측 데이터의 경과 시간(Observation Age), 명령 경과 시간(Command Age), 최악 실행시간(Worst-Case Execution Time)을 측정해야 한다.

배치된 추론 엔진(Inference Engine)은 검증된 학습 구현과의 수치적 동등성(Numerical Equivalence)이 입증된 이후에만 고정해야 한다. 모델 내보내기(Model Export), 그래프 최적화(Graph Optimization), TensorRT 변환, FP16 실행 또는 기타 가속 기법은 수치적 동작을 변화시킬 수 있다. 따라서 대표적인 관측 데이터 세트를 두 구현에서 모두 재생하고, 행동 차이가 명시적으로 정의된 허용 오차(Accepted Tolerance) 이내에 존재하는지 확인한 후 하드웨어용으로 릴리스해야 한다.

안전 감독(Safety Supervision)은 강화학습 정책과 독립적으로 유지되어야 한다. 관절 위치, 속도, 토크, 몸체 자세(Body Orientation), 액추에이터 온도, 배터리 상태, 통신 상태, 센서 유효성(Sensor Validity), 충돌 조건, 제어 데드라인을 신경망 외부에서 모니터링할 수 있다. 한계값을 초과하면 감독 계층(Supervisory Layer)은 명령 제한, 속도 감소, 자세 전환(Posture Transition), 대체 제어기(Fallback Controller) 호출 또는 비상 정지(Emergency Stop)를 수행할 수 있어야 한다.

제품 배치를 위해서는 명확하게 정의된 운용 상태(Operational State)도 필요하다. 시작(Startup), 초기화(Initialization), 기립(Standing), 보행(Locomotion), 성능 저하 운용(Degraded Operation), 복구, 종료(Shutdown), 비상 동작(Emergency Behavior) 사이의 전환은 결정론적으로 정의되어야 한다. 필요한 센서, 상태 추정(State Estimation), 액추에이터 통신, 정규화 데이터, 런타임 구성이 검증되기 전에는 정책이 로봇 제어를 시작해서는 안 된다. 마찬가지로 필수적인 구성 요소를 사용할 수 없게 되면 안전하게 제어를 종료해야 한다.

이전 행동, 순환 상태(Recurrent State) 또는 관측 이력을 사용하는 정책에서는 시작 초기화(Startup Initialization)가 특히 중요하다. 버퍼(Buffer)는 임의의 런타임 값으로 채우는 것이 아니라 학습 과정에서 사용한 가정에 따라 초기화해야 한다. 기립 상태에서 학습 기반 보행으로 제어된 전환(Controlled Transition)을 수행하면 최초 정책 주기에서 관절 목표와 내부 시간 상태(Internal Temporal State)가 불연속적으로 변화하는 것을 방지할 수 있다.

고장 처리(Fault Handling)는 일시적인 이상과 즉각적인 종료가 필요한 상태를 구분해야 한다. 한 번의 관측 지연은 제한된 대체 응답(Bounded Fallback Response)으로 처리할 수 있지만, 반복적으로 오래된 데이터(Stale Data)가 입력되거나 잘못된 상태 추정, NaN 정책 출력, 통신 손실, 심각한 자세 오차 또는 액추에이터 고장이 발생하면 보행을 종료해야 할 수 있다. 각 고장 유형에 대한 대응은 결정론적이고 시험 가능하며 기록되어야 하고 작업자의 주관적인 판단에 의존해서는 안 된다.

복구 동작(Recovery Behavior)은 일반적인 학습 기반 외란 복구(Learned Disturbance Rejection)를 넘어 별도로 정의되어야 한다. 정책은 학습 분포 내부에서 발생하는 미끄러짐, 충격 또는 일시적인 지형 오류로부터 복구할 수 있지만 큰 실패는 로봇을 해당 분포 밖의 상태로 이동시킬 수 있다. 따라서 제품 시스템에는 안전 정지(Safe Stopping), 제어된 앉기 또는 눕기, 기립 복구(Stand-Up Recovery), 작업자 개입(Operator Intervention), 다른 검증된 제어기로의 전환과 같은 별도의 절차가 필요하다.

검증(Validation)은 점진적으로 현실적인 단계로 진행해야 한다. 오프라인 모델 재생(Offline Model Replay)을 통해 수치적 동작을 검증하고, 소프트웨어 인 더 루프 시험(Software-in-the-Loop Testing)을 통해 인터페이스를 확인하며, 하드웨어 인 더 루프 시험(Hardware-in-the-Loop Testing)을 통해 실제 제품 통신 경로를 검증할 수 있다. 이후 제한된 로봇 시험으로 실제 물리적 실행을 확인하고, 이러한 단계가 완료된 후에만 더 높은 속도, 어려운 지형, 페이로드 변화, 환경 외란, 장시간 자율 임무로 시험 범위를 확대해야 한다.

승인 기준(Acceptance Criteria)은 주로 시각적 판단에 의존하는 것이 아니라 정량적으로 정의되어야 한다. 명령 추종 오차(Command-Tracking Error), 전도 빈도(Fall Frequency), 지형 통과 성능(Terrain Completion), 복구 성공률(Recovery Success), 발 미끄러짐(Foot Slip), 에너지 소비, 액추에이터 포화(Actuator Saturation), 몸체 진동(Body Oscillation), 추론 지연시간, 데드라인 미준수율(Deadline-Miss Rate), 안전 개입(Safety Intervention)을 이용하여 제품 준비 상태(Production Readiness)를 평가할 수 있다. 단 한 번의 성공적인 시연은 운용 신뢰성에 대한 충분한 증거가 되지 않으므로 반복 시험을 통해 지표를 평가해야 한다.

장시간 시험(Long-Duration Testing)은 짧은 보행 시연에서 발견하기 어려운 고장 형태를 드러낸다. 열 스로틀링(Thermal Throttling), 배터리 전압 저하, 메모리 증가(Memory Growth), 통신 성능 저하, 추정기 드리프트(Estimator Drift), 기계적 발열, 보정 변화(Calibration Change), 누적된 타이밍 교란이 지속적인 운용 이후에만 나타날 수 있다. 따라서 제품 적격성 검증(Production Qualification)에는 지각, 내비게이션, 로깅, 통신 작업을 동시에 실행하는 실제 임무 시간 수준의 시험이 포함되어야 한다.

환경 검증(Environmental Validation)은 목표로 하는 실제 운용 범위(Operational Envelope)를 반영해야 한다. 제품용 사족보행 로봇은 매끄러운 바닥, 램프(Ramp), 계단, 자갈, 불규칙한 야외 지면, 저마찰 영역(Low-Friction Region), 장애물, 페이로드 변화, 외부 외란을 경험할 수 있다. 시험에는 정상 조건, 경계 조건(Boundary Condition), 정상 한계를 넘어서는 통제된 조건을 포함하여 어느 지점에서 성능이 저하되고 어느 지점에서 안전 감독 기능이 개입해야 하는지를 확인해야 한다.

여러 대의 실제 로봇을 배치하는 경우 구성 관리(Configuration Management)는 더욱 중요해진다. 하드웨어 개정(Revision), 액추에이터 보정(Actuator Calibration), 센서 외부 파라미터(Sensor Extrinsic), 페이로드 구성, 펌웨어 버전(Firmware Version), 추론 엔진의 차이는 외형상 동일한 로봇 사이에서도 의미 있는 성능 차이를 발생시킬 수 있다. 따라서 각 정책 릴리스(Policy Release)는 검증된 호환 범위를 명확하게 지정해야 하며, 배치 도구는 지원되지 않는 조합이 실수로 설치되는 것을 방지해야 한다.

텔레메트리(Telemetry)와 로깅은 현장 진단(Field Diagnosis)에 필요한 근거를 제공한다. 제품 로그에는 관련 관측값, 명령, 행동, 상태 추정값, 추론 타이밍, 안전 이벤트(Safety Event), 액추에이터 상태, 소프트웨어 버전을 동기화된 타임스탬프와 함께 기록해야 한다. 문제가 발생하면 엔지니어가 원인이 지각, 상태 추정, 정책 동작, 타이밍, 통신, 하드웨어 또는 환경 조건 중 어디에서 발생했는지를 재구성할 수 있어야 한다.

현장 데이터(Field Data)는 실제 배치를 자동으로 온라인 강화학습(Online Reinforcement Learning)으로 전환하지 않으면서 시뮬레이션에 다시 반영해야 한다. 반복적인 미끄러짐, 타이밍 이상, 액추에이터 차이, 페이로드 영향 또는 지형 실패 사례를 이용하여 시스템 식별(System Identification), 도메인 무작위화 범위(Domain-Randomization Range), 지형 분포(Terrain Distribution), 검증 시나리오를 개선할 수 있다. 이후 수정된 정책을 다시 학습하고 통제된 릴리스 절차를 통해 적격성을 검증한 후 기존 제품 정책을 교체할 수 있다.

정책 업데이트(Policy Update)에는 회귀 시험(Regression Testing)이 필요하다. 특정 지형이나 명령 범위에서 성능이 향상되더라도 이전에 검증된 동작의 성능이 저하될 수 있기 때문이다. 새로운 릴리스는 대표적인 명령, 지형, 외란, 하드웨어 변화, 안전 사례를 포함하는 고정된 벤치마크 시험군(Benchmark Suite)을 이용하여 평가해야 한다. 현재 배치된 정책과 비교하면 성능 변화를 명확하게 확인할 수 있으며 재학습 과정에서 기존 기능이 조용히 손실되는 위험을 줄일 수 있다.

롤백 기능(Rollback Capability) 역시 중요하다. 새로운 릴리스에서 예상하지 못한 현장 동작이 발생할 경우 이전에 검증된 정책, 런타임 엔진(Runtime Engine), 정규화 구성, 관련 소프트웨어를 다시 사용할 수 있어야 한다. 따라서 모델 배치는 식별 가능한 버전(Identifiable Version)과 재현 가능한 패키지(Reproducible Package)를 사용해야 하며, 개별 로봇에서 추적성(Traceability) 없이 신경망 파일을 수동으로 교체하는 방식은 피해야 한다.

궁극적으로 제품 준비 상태(Production Readiness)는 강화학습 정책이 전체 로봇 시스템 내부에서 통제되는 하나의 구성 요소로 동작한다는 것을 의미한다. PPO 학습, 보상 공학(Reward Engineering), 지형 커리큘럼(Terrain Curriculum), 특권 학습(Privileged Learning), 액추에이터 모델링(Actuator Modeling), 도메인 무작위화(Domain Randomization), 제로샷 시뮬레이션-현실 전이(Zero-Shot Sim2Real Transfer), 온보드 추론(Onboard Inference)은 기술적 능력을 확립한다. 제품 배치 공학(Deployment Engineering)은 이러한 능력을 안전하고 일관되게 유지하기 위해 필요한 수명주기 관리(Lifecycle Control)를 추가한다.

따라서 제품용 보행 정책(Production Locomotion Policy)은 로봇이 시뮬레이션 외부에서 처음 성공적으로 걷는 순간 완성되는 것이 아니다. 입력, 출력, 타이밍, 하드웨어 의존성(Hardware Dependency), 안전 경계(Safety Boundary), 고장 대응(Failure Response), 검증 근거(Validation Evidence), 텔레메트리, 버전 이력(Version History), 업데이트 절차가 반복 운용에 충분할 정도로 통제될 때 비로소 완성된다. 이를 통해 강화학습 기반 보행은 실험적인 시연(Experimental Demonstration)에서 실제 배치 가능한 피지컬 AI 인프라(Deployable Physical AI Infrastructure)로 전환된다.
