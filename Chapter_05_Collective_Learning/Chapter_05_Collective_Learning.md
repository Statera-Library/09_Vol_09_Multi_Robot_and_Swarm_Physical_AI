**Volume 09. Multi Robot and Swarm Physical AI**


# Chapter 05. Collective Learning

##  

## 05.01. From Individual to Collective Learning

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

Individual robot learning focuses on improving the behavior of a single embodied agent from its own observations, actions, rewards, demonstrations, and interaction history. Collective learning extends this principle across multiple robots so that experience acquired by one member can contribute to the competence of others. In a multi-robot Physical AI system, the learning unit therefore evolves from an isolated robot into a connected population of agents that accumulate knowledge together.

This transition changes the fundamental economics of robot learning. A single robot can experience only a limited number of environments, failures, objects, terrain conditions, and task variations during a given period. A fleet can collect many experiences simultaneously. When those experiences are aggregated appropriately, hundreds of robot-hours can be transformed into shared training data during one hour of fleet operation, dramatically increasing the diversity and rate of learning.

Collective learning does not require every robot to execute exactly the same policy or maintain an identical internal model. Each robot may preserve local knowledge associated with its embodiment, sensors, operational environment, or assigned role while contributing transferable information to a shared learning process. The objective is to separate knowledge that is generally useful across the fleet from knowledge that should remain specific to particular robots, tasks, or environments.

A useful abstraction is to consider each robot as both an actor and a data-generating learning node. During operation, robots perceive the physical environment, select actions, observe outcomes, and generate trajectories containing states, observations, actions, rewards, failures, interventions, and task results. These local experiences become potential learning resources rather than disappearing after execution, allowing operational activity to continuously enlarge the collective experience of the fleet.

The simplest transition from individual to collective learning occurs through centralized experience aggregation. Robots upload selected trajectories to a common repository where data can be filtered, normalized, labeled, ranked, or converted into training samples. A shared model is then trained using experience gathered across the population and redistributed to individual robots. Although conceptually straightforward, this approach establishes the essential feedback loop between fleet operation, data collection, learning, and deployment.

The value of collective experience is not determined only by its volume. Different robots frequently encounter different portions of the operational distribution. One warehouse robot may discover congestion patterns, another may experience unusual payload dynamics, and another may encounter difficult perception conditions. Combining these experiences broadens the learning distribution and allows the resulting system to acquire capabilities that would be difficult for any individual robot to obtain through isolated operation.

Failure experience is particularly important because successful operation often produces repetitive and predictable data. Rare collisions, localization degradation, manipulation failures, communication losses, difficult terrain, unusual objects, and human interventions can contain disproportionately valuable information. Collective learning enables these uncommon events to be captured across many robots and converted into shared knowledge, allowing one robot\'s difficult encounter to reduce the probability that other robots repeat the same failure.

Collective learning also introduces the distinction between experience sharing and knowledge sharing. Raw sensor streams and trajectories can be exchanged as experience, but communication and storage constraints may make continuous transmission impractical. Robots can instead share compressed representations, learned parameters, gradients, embeddings, policies, skills, maps, statistics, or selected episodes. The appropriate representation depends on whether the fleet is optimizing bandwidth, privacy, training efficiency, adaptation speed, or cross-robot compatibility.

Physical embodiment makes this process more difficult than collective learning among purely digital agents. Robots may have different cameras, LiDAR configurations, manipulators, mobility systems, payload limits, control frequencies, and action spaces. Even nominally identical robots gradually develop different calibration states and mechanical characteristics. Consequently, collective learning requires representations that distinguish transferable task knowledge from embodiment-specific information that cannot safely be copied directly between platforms.

A major architectural choice concerns where learning occurs. Training may be centralized on an on-premise or cloud computing system, distributed across robots, or divided between fleet infrastructure and onboard processors. Centralized training provides access to large aggregated datasets and substantial compute resources, while distributed approaches preserve locality and reduce raw-data transfer. Hybrid architectures can combine fleet-scale model improvement with rapid local adaptation during physical operation.

Collective learning must also address non-stationarity. As robots learn and updated policies are deployed, the behavior of the fleet changes, which in turn changes the data generated by future interactions. Experience collected under an older navigation or coordination policy may not represent the distribution produced by a newer one. Dataset versioning, policy identification, temporal metadata, evaluation, and controlled deployment therefore become important components of the collective learning lifecycle.

Trust is equally important because not every observation or update should influence the fleet equally. Sensor faults, corrupted localization, unusual operating conditions, poorly calibrated robots, or unsuccessful experiments can introduce misleading knowledge. Collective systems therefore benefit from confidence estimates, provenance information, validation procedures, and quality weighting. Shared learning should aggregate useful evidence while preventing unreliable local experience from degrading the behavior of the wider population.

The relationship between individual and collective learning is therefore bidirectional rather than hierarchical. Individual robots provide the physical experiences from which collective knowledge emerges, while the collective system returns improved models, policies, representations, or skills to individual robots. Those robots then generate new experiences under improved behavior, producing another learning cycle. This repeated exchange creates a continuously evolving connection between local interaction and fleet-level intelligence.

Such a cycle provides the foundation for more advanced mechanisms developed throughout collective learning, including shared robot knowledge, centralized training with distributed execution, multi-agent reinforcement learning, cooperative imitation learning, federated learning, distributed model updates, skill sharing, cross-robot experience replay, transfer learning, and continual learning. These mechanisms represent different solutions to the same fundamental problem: converting distributed physical experience into reusable collective intelligence.

At fleet scale, the long-term result is a data flywheel in which deployment itself becomes part of the learning infrastructure. More robots create more diverse physical experience; better experience supports stronger models; stronger models improve robot performance; improved performance enables broader deployment; and broader deployment generates still more experience. Collective learning therefore transforms a robot fleet from a collection of independently improving machines into a distributed Physical AI system whose operational history becomes a continuously expanding source of intelligence.

개별 로봇 학습(Individual Robot Learning)은 하나의 체화된 에이전트(Embodied Agent)가 자신의 관측(Observation), 행동(Action), 보상(Reward), 시연(Demonstration), 상호작용 이력(Interaction History)을 이용하여 행동 성능을 향상시키는 데 초점을 둔다. 집단 학습(Collective Learning)은 이러한 원리를 여러 로봇으로 확장하여 한 구성원이 획득한 경험이 다른 로봇의 역량 향상에도 기여하도록 한다. 따라서 다중 로봇 피지컬 AI(Multi-Robot Physical AI) 시스템에서는 학습 단위가 고립된 개별 로봇에서 공동으로 지식을 축적하는 연결된 에이전트 집단으로 발전한다.

이러한 전환은 로봇 학습(Robot Learning)의 근본적인 경제성을 변화시킨다. 단일 로봇(Single Robot)은 일정한 시간 동안 제한된 수의 환경, 실패, 객체, 지형 조건, 작업 변형만을 경험할 수 있다. 반면 로봇 플릿(Robot Fleet)은 다수의 경험을 동시에 수집할 수 있다. 이러한 경험을 적절하게 통합하면 실제 한 시간의 플릿 운영을 통해 수백 로봇-시간(Robot-Hours)에 해당하는 공유 학습 데이터를 확보할 수 있으며, 학습의 다양성과 속도를 크게 향상시킬 수 있다.

집단 학습(Collective Learning)은 모든 로봇이 정확히 동일한 정책(Policy)을 실행하거나 동일한 내부 모델(Internal Model)을 유지해야 한다는 것을 의미하지 않는다. 각 로봇은 자신의 체화(Embodiment), 센서(Sensor), 운영 환경(Operational Environment), 할당된 역할과 관련된 로컬 지식(Local Knowledge)을 유지하면서 공유 학습 과정에 활용할 수 있는 정보를 제공할 수 있다. 핵심 목적은 플릿 전체에서 일반적으로 활용할 수 있는 지식과 특정 로봇, 작업 또는 환경에 한정되어야 하는 지식을 구분하는 것이다.

유용한 추상화 방식은 각각의 로봇을 행동 주체(Actor)이면서 동시에 데이터를 생성하는 학습 노드(Learning Node)로 간주하는 것이다. 로봇은 운영 과정에서 물리 환경(Physical Environment)을 인식하고, 행동을 선택하며, 결과를 관찰하고, 상태(State), 관측, 행동, 보상, 실패, 개입(Intervention), 작업 결과를 포함하는 궤적(Trajectory)을 생성한다. 이러한 로컬 경험(Local Experience)은 실행 이후 사라지는 정보가 아니라 잠재적인 학습 자원이 되어 플릿의 집단 경험을 지속적으로 확장한다.

개별 학습(Individual Learning)에서 집단 학습으로 전환하는 가장 단순한 방법은 중앙집중식 경험 통합(Centralized Experience Aggregation)이다. 로봇은 선택된 궤적을 공통 저장소(Common Repository)에 업로드하고, 여기에서 데이터를 필터링, 정규화, 라벨링, 순위화하거나 학습 샘플로 변환한다. 이후 전체 로봇 집단에서 수집한 경험으로 공유 모델(Shared Model)을 학습하고 이를 다시 개별 로봇에 배포한다. 이 방식은 개념적으로 단순하지만 플릿 운영, 데이터 수집, 학습, 배포를 연결하는 핵심 피드백 루프(Feedback Loop)를 형성한다.

집단 경험(Collective Experience)의 가치는 단순히 데이터의 양에 의해서만 결정되지 않는다. 서로 다른 로봇은 운영 분포(Operational Distribution)의 서로 다른 영역을 경험하는 경우가 많다. 하나의 창고 로봇은 혼잡 패턴(Congestion Pattern)을 발견하고, 다른 로봇은 특이한 적재물 동역학(Payload Dynamics)을 경험하며, 또 다른 로봇은 어려운 인식 조건(Perception Condition)에 직면할 수 있다. 이러한 경험을 결합하면 학습 분포를 확장하여 개별 로봇이 독립적인 운영만으로 획득하기 어려운 역량을 학습할 수 있다.

실패 경험(Failure Experience)은 성공적인 운영에서 반복적이고 예측 가능한 데이터가 많이 생성되기 때문에 특히 중요하다. 드문 충돌, 위치추정 성능 저하(Localization Degradation), 조작 실패(Manipulation Failure), 통신 손실(Communication Loss), 험난한 지형, 비정상적인 객체, 인간 개입(Human Intervention)은 상대적으로 높은 학습 가치를 가질 수 있다. 집단 학습은 여러 로봇에서 이러한 희귀 사건을 수집하고 공유 지식으로 변환하여 하나의 로봇이 경험한 어려움이 다른 로봇에서 동일한 실패가 반복될 가능성을 낮추도록 한다.

집단 학습은 경험 공유(Experience Sharing)와 지식 공유(Knowledge Sharing)를 구분하는 개념도 도입한다. 원시 센서 스트림(Raw Sensor Stream)과 궤적 자체를 경험으로 교환할 수 있지만, 통신 및 저장장치의 제약으로 모든 데이터를 지속적으로 전송하는 것은 현실적으로 어려울 수 있다. 따라서 로봇은 압축 표현(Compressed Representation), 학습된 파라미터(Learned Parameter), 그래디언트(Gradient), 임베딩(Embedding), 정책, 기술(Skill), 지도(Map), 통계 또는 선택된 에피소드(Episode)를 공유할 수 있다. 적절한 표현은 대역폭, 프라이버시, 학습 효율, 적응 속도, 로봇 간 호환성 가운데 무엇을 최적화하는지에 따라 달라진다.

물리적 체화(Physical Embodiment)는 순수한 디지털 에이전트(Digital Agent) 사이의 집단 학습보다 이 과정을 어렵게 만든다. 로봇마다 카메라, 라이다(LiDAR), 매니퓰레이터(Manipulator), 이동 시스템(Mobility System), 적재 한계(Payload Limit), 제어 주기(Control Frequency), 행동 공간(Action Space)이 서로 다를 수 있다. 동일한 모델의 로봇도 시간이 지나면서 캘리브레이션 상태(Calibration State)와 기계적 특성이 달라진다. 따라서 집단 학습에서는 플랫폼 간 직접 복사가 불가능한 체화 특화 정보(Embodiment-Specific Information)와 전이 가능한 작업 지식(Transferable Task Knowledge)을 구분할 수 있는 표현이 필요하다.

중요한 아키텍처 선택 가운데 하나는 학습이 어디에서 이루어지는가이다. 학습은 온프레미스(On-Premise) 또는 클라우드 컴퓨팅(Cloud Computing) 시스템에서 중앙집중식으로 수행하거나, 여러 로봇에 분산하거나, 플릿 인프라와 온보드 프로세서(Onboard Processor) 사이에 분할할 수 있다. 중앙집중식 학습(Centralized Training)은 대규모 통합 데이터셋과 높은 연산 성능을 활용할 수 있으며, 분산 방식(Distributed Approach)은 데이터의 로컬성을 유지하고 원시 데이터 전송량을 줄일 수 있다. 하이브리드 아키텍처(Hybrid Architecture)는 플릿 규모의 모델 개선과 실제 운영 중의 빠른 로컬 적응(Local Adaptation)을 결합할 수 있다.

집단 학습은 비정상성(Non-Stationarity) 문제도 해결해야 한다. 로봇이 학습하고 업데이트된 정책이 배포되면 플릿의 행동이 변화하며, 이에 따라 이후 상호작용에서 생성되는 데이터의 특성도 변화한다. 이전 내비게이션(Navigation) 또는 협조 정책(Coordination Policy)에서 수집한 경험은 새로운 정책에서 생성되는 분포를 정확하게 대표하지 못할 수 있다. 따라서 데이터셋 버전 관리(Dataset Versioning), 정책 식별(Policy Identification), 시간 메타데이터(Temporal Metadata), 평가(Evaluation), 통제된 배포(Controlled Deployment)가 집단 학습 생명주기의 중요한 구성요소가 된다.

모든 관측이나 업데이트가 플릿 전체에 동일한 영향을 주어서는 안 되기 때문에 신뢰(Trust) 역시 중요하다. 센서 고장, 손상된 위치추정, 비정상적인 운영 조건, 잘못 캘리브레이션된 로봇, 실패한 실험은 잘못된 지식을 유입할 수 있다. 따라서 집단 시스템(Collective System)은 신뢰도 추정(Confidence Estimation), 출처 정보(Provenance Information), 검증 절차(Validation Procedure), 품질 가중치(Quality Weighting)를 활용할 수 있다. 공유 학습은 유용한 증거를 통합하는 동시에 신뢰할 수 없는 로컬 경험이 전체 로봇 집단의 행동을 저하시키는 것을 방지해야 한다.

따라서 개별 학습과 집단 학습의 관계는 계층적(Hierarchical)이라기보다 양방향적(Bidirectional)이다. 개별 로봇은 집단 지식(Collective Knowledge)이 형성되는 물리적 경험을 제공하고, 집단 시스템은 개선된 모델, 정책, 표현 또는 기술을 다시 개별 로봇에 제공한다. 이후 로봇들은 개선된 행동을 기반으로 새로운 경험을 생성하며 또 다른 학습 주기를 형성한다. 이러한 반복적인 교환은 로컬 상호작용(Local Interaction)과 플릿 수준 지능(Fleet-Level Intelligence)을 연결하는 지속적으로 진화하는 구조를 만든다.

이러한 순환 구조는 공유 로봇 지식(Shared Robot Knowledge), 중앙집중식 학습과 분산 실행(Centralized Training with Distributed Execution), 다중 에이전트 강화학습(Multi-Agent Reinforcement Learning), 협력적 모방학습(Cooperative Imitation Learning), 연합학습(Federated Learning), 분산 모델 업데이트(Distributed Model Updates), 기술 공유(Skill Sharing), 로봇 간 경험 재현(Cross-Robot Experience Replay), 전이학습(Transfer Learning), 지속학습(Continual Learning)과 같은 더욱 발전된 집단 학습 메커니즘의 기반이 된다. 이들은 분산된 물리적 경험을 재사용 가능한 집단 지능(Collective Intelligence)으로 변환한다는 동일한 근본 문제에 대한 서로 다른 해결 방식이다.

플릿 규모(Fleet Scale)에서 장기적인 결과는 실제 배포 자체가 학습 인프라의 일부가 되는 데이터 플라이휠(Data Flywheel)이다. 더 많은 로봇은 더욱 다양하고 풍부한 물리적 경험을 생성하고, 더 나은 경험은 더욱 강력한 모델을 만들며, 향상된 모델은 로봇의 성능을 개선한다. 성능 향상은 더 광범위한 배포를 가능하게 하고, 확대된 배포는 다시 더 많은 경험을 생성한다. 따라서 집단 학습은 로봇 플릿을 독립적으로 학습하는 기계들의 집합에서 운영 이력 자체가 지속적으로 확장되는 지능의 원천이 되는 분산형 피지컬 AI(Distributed Physical AI) 시스템으로 발전시킨다.

##  

## 05.02. Shared Experience and Robot Knowledge

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

Shared experience allows a multi-robot system to transform isolated physical interactions into reusable knowledge for the entire fleet. Each robot continuously encounters objects, terrain, people, tasks, failures, and environmental changes that other robots may not yet have experienced. When these observations and outcomes are captured and shared, local experience becomes a collective resource rather than knowledge that remains confined to the robot that originally acquired it.

Robot experience can be represented as trajectories that connect observations, internal states, actions, and resulting outcomes over time. A navigation trajectory may contain sensor observations, estimated poses, selected paths, control commands, obstacle encounters, and mission results. Manipulation experience may additionally include object states, grasp attempts, forces, contact events, and success or failure information. These structured histories provide the raw material from which reusable robot knowledge can be extracted.

Not every piece of experience has equal value for collective learning. Repeated successful operations in familiar environments may provide limited new information, whereas rare failures, unexpected obstacles, unusual terrain, localization errors, human interventions, or recovery behaviors can be highly informative. A shared experience system therefore benefits from mechanisms that identify novelty, uncertainty, difficulty, failure, and unusual outcomes so that valuable episodes receive greater attention during storage and learning.

Raw experience and robot knowledge should be distinguished conceptually. Experience describes what a robot observed and what happened during interaction, while knowledge represents information extracted or generalized from those experiences. Thousands of navigation trajectories, for example, may eventually produce knowledge about traversable regions, congestion patterns, obstacle risks, localization reliability, or effective recovery strategies. Collective learning converts distributed experience into representations that can guide future decisions.

Shared robot knowledge can exist at several levels of abstraction. At a low level, robots may exchange sensor features, calibration information, motion statistics, or local environmental observations. At intermediate levels, they may share semantic maps, object representations, traversability estimates, task outcomes, or learned skills. At higher levels, the fleet may distribute policies, models, embeddings, planning heuristics, task strategies, or generalized representations that summarize experience collected across many robots.

Spatial knowledge is especially valuable because physical robots operate in environments whose geometry and semantics strongly influence behavior. One robot may discover a blocked corridor, slippery surface, narrow passage, charging location, temporary construction area, or frequently occupied region. Sharing such information allows other robots to incorporate previously acquired environmental knowledge into planning before directly encountering the same condition, improving efficiency and reducing unnecessary exploration.

Experience sharing also supports knowledge about dynamic environments. A physical workspace is rarely static: people move, inventory changes, doors open and close, equipment is relocated, and traffic conditions vary with time. Shared knowledge must therefore include temporal context rather than treating every observation as permanently valid. Time stamps, observation frequency, confidence, and update history help determine whether previously acquired information should remain active, be revised, or gradually lose importance.

A practical fleet cannot transmit every sensor frame generated by every robot. Cameras, LiDARs, tactile sensors, and other modalities can produce enormous data volumes, while wireless networks have finite bandwidth and intermittent connectivity. Shared experience architectures consequently require selection and compression. Robots may upload important episodes, event-triggered records, compact features, semantic summaries, learned parameters, or metadata instead of continuously transferring complete raw sensor streams.

Knowledge provenance becomes important once information from many robots is combined. The system should ideally know which robot generated an observation, when and where it was acquired, which sensors and software versions were involved, and under what operating conditions it occurred. Provenance enables later validation and debugging and prevents shared knowledge from becoming an anonymous collection of information whose reliability, origin, and relevance cannot be determined.

Confidence must accompany shared knowledge because different observations may have different reliability. A robot with degraded localization or contaminated sensors should not influence fleet knowledge as strongly as a robot operating with high-confidence perception. Shared representations can therefore associate observations with uncertainty, confidence scores, quality indicators, or validation status. Knowledge fusion then becomes a process of combining evidence according to both information content and estimated reliability.

Conflicting knowledge is inevitable in distributed physical systems. Two robots may classify the same terrain differently, report different object positions, or observe an environment at different times. Such disagreement does not necessarily indicate that one robot is wrong because the physical world may have changed between observations. Collective systems must compare timestamps, confidence, context, sensor capabilities, and environmental dynamics before deciding whether information should be merged, replaced, retained separately, or marked as uncertain.

Shared experience becomes particularly powerful when it includes success, failure, and recovery together. A fleet that records only successful trajectories learns what normally works but receives limited information about operational boundaries. Failure episodes reveal conditions under which policies break down, while recovery episodes demonstrate how robots can return to safe or productive states. Together these experiences support more robust navigation, manipulation, coordination, and autonomous decision making.

Heterogeneous fleets make knowledge sharing more challenging because robots may possess different embodiments and capabilities. Experience from an AMR, quadruped, manipulator, humanoid, or UAV cannot always be transferred directly because their sensing and action spaces differ. Nevertheless, higher-level knowledge about objects, hazards, task structure, spatial relationships, semantic environments, and mission outcomes may remain transferable when represented independently from platform-specific control commands.

Shared knowledge can therefore be organized into common and robot-specific components. Common knowledge describes information that is broadly useful across the fleet, while robot-specific knowledge captures embodiment, sensor configuration, payload, mobility, calibration, or operational constraints. This separation allows collective intelligence to benefit from diverse experience without assuming that every robot can perform every action or interpret every observation in exactly the same way.

The overall process forms a continuous knowledge lifecycle. Robots generate experience during physical operation, select valuable observations, attach contextual and confidence information, and contribute them to shared storage or distributed learning mechanisms. The fleet then filters, aggregates, validates, and transforms this experience into reusable knowledge, which is distributed back to robots and applied to future perception, planning, task execution, and learning.

Shared experience and robot knowledge therefore provide the informational foundation for collective learning. They connect individual physical interaction with fleet-scale intelligence and prepare the architecture for centralized training and distributed execution, multi-agent reinforcement learning, federated robot learning, distributed model updates, policy and skill sharing, cross-robot experience replay, and transfer learning. As deployment grows, every robot can become both a consumer and a producer of knowledge for the wider Physical AI fleet.

공유 경험(Shared Experience)은 다중 로봇 시스템(Multi-Robot System)이 개별적으로 발생한 물리적 상호작용을 전체 플릿(Fleet)이 재사용할 수 있는 지식으로 변환하도록 한다. 각 로봇은 다른 로봇이 아직 경험하지 못한 객체, 지형, 사람, 작업, 실패, 환경 변화를 지속적으로 경험한다. 이러한 관측과 결과를 기록하고 공유하면 로컬 경험(Local Experience)은 이를 최초로 획득한 로봇에만 머무는 지식이 아니라 집단 전체가 활용할 수 있는 자원이 된다.

로봇 경험(Robot Experience)은 시간에 따른 관측(Observation), 내부 상태(Internal State), 행동(Action), 그리고 그 결과를 연결하는 궤적(Trajectory)으로 표현할 수 있다. 내비게이션 궤적(Navigation Trajectory)은 센서 관측, 추정 위치, 선택 경로, 제어 명령, 장애물 조우, 임무 결과를 포함할 수 있다. 조작 경험(Manipulation Experience)은 객체 상태, 파지 시도, 힘, 접촉 사건, 성공 또는 실패 정보를 추가로 포함할 수 있다. 이러한 구조화된 이력은 재사용 가능한 로봇 지식을 추출하기 위한 원천 자료가 된다.

모든 경험이 집단 학습(Collective Learning)에 동일한 가치를 가지는 것은 아니다. 익숙한 환경에서 반복되는 성공적인 운영은 새로운 정보를 거의 제공하지 못할 수 있지만, 드문 실패, 예상하지 못한 장애물, 특이한 지형, 위치추정 오류(Localization Error), 인간 개입(Human Intervention), 복구 행동(Recovery Behavior)은 매우 유용한 정보를 제공할 수 있다. 따라서 공유 경험 시스템은 새로움, 불확실성, 난이도, 실패, 비정상적인 결과를 식별하여 가치가 높은 에피소드(Episode)가 저장과 학습 과정에서 더 높은 중요도를 갖도록 하는 메커니즘이 필요하다.

원시 경험(Raw Experience)과 로봇 지식(Robot Knowledge)은 개념적으로 구분해야 한다. 경험은 로봇이 무엇을 관측했으며 상호작용 과정에서 어떤 일이 발생했는지를 나타내는 반면, 지식은 이러한 경험으로부터 추출되거나 일반화된 정보를 의미한다. 예를 들어 수천 개의 내비게이션 궤적은 궁극적으로 주행 가능 영역(Traversable Region), 혼잡 패턴(Congestion Pattern), 장애물 위험, 위치추정 신뢰성, 효과적인 복구 전략에 관한 지식으로 발전할 수 있다. 집단 학습은 분산된 경험을 미래 의사결정을 지원하는 표현(Representation)으로 변환한다.

공유 로봇 지식(Shared Robot Knowledge)은 여러 추상화 수준에서 존재할 수 있다. 낮은 수준에서는 센서 특징(Sensor Feature), 캘리브레이션 정보(Calibration Information), 운동 통계(Motion Statistics), 로컬 환경 관측을 교환할 수 있다. 중간 수준에서는 의미론적 지도(Semantic Map), 객체 표현(Object Representation), 주행 가능성 추정(Traversability Estimation), 작업 결과, 학습된 기술(Skill)을 공유할 수 있다. 높은 수준에서는 여러 로봇에서 수집한 경험을 요약한 정책(Policy), 모델(Model), 임베딩(Embedding), 계획 휴리스틱(Planning Heuristic), 작업 전략 또는 일반화된 표현을 플릿 전체에 배포할 수 있다.

공간 지식(Spatial Knowledge)은 물리적 로봇이 행동하는 환경의 기하학적 구조와 의미론적 특성이 행동에 큰 영향을 미치기 때문에 특히 중요하다. 하나의 로봇이 차단된 통로, 미끄러운 표면, 좁은 구간, 충전 위치, 임시 공사 구역 또는 자주 혼잡해지는 영역을 발견할 수 있다. 이러한 정보를 공유하면 다른 로봇은 동일한 조건을 직접 경험하기 전에 기존 환경 지식을 계획(Planning)에 반영할 수 있으며, 이를 통해 효율성을 높이고 불필요한 탐색을 줄일 수 있다.

경험 공유(Experience Sharing)는 동적 환경(Dynamic Environment)에 관한 지식도 지원한다. 물리적 작업 공간은 거의 정적인 상태로 유지되지 않으며 사람은 이동하고, 재고는 변경되고, 문은 열리고 닫히며, 장비 위치와 교통 상황도 시간에 따라 달라진다. 따라서 공유 지식은 모든 관측을 영구적으로 유효한 것으로 취급하지 않고 시간적 맥락(Temporal Context)을 포함해야 한다. 타임스탬프(Time Stamp), 관측 빈도, 신뢰도(Confidence), 업데이트 이력은 기존 정보가 계속 유지되어야 하는지, 수정되어야 하는지 또는 점진적으로 중요도를 낮춰야 하는지를 판단하는 데 활용된다.

실제 플릿은 모든 로봇이 생성하는 모든 센서 프레임을 전송할 수 없다. 카메라, 라이다(LiDAR), 촉각 센서(Tactile Sensor) 등의 센서는 막대한 데이터량을 생성할 수 있지만 무선 네트워크의 대역폭은 제한적이며 연결 상태도 간헐적으로 불안정할 수 있다. 따라서 공유 경험 아키텍처(Shared Experience Architecture)에는 데이터 선택과 압축(Compression)이 필요하다. 로봇은 전체 원시 센서 스트림을 지속적으로 전송하는 대신 중요한 에피소드, 이벤트 기반 기록(Event-Triggered Record), 압축 특징(Compact Feature), 의미론적 요약(Semantic Summary), 학습된 파라미터 또는 메타데이터(Metadata)를 업로드할 수 있다.

여러 로봇에서 생성된 정보가 결합되면 지식 출처 추적(Knowledge Provenance)이 중요해진다. 시스템은 어떤 로봇이 관측을 생성했는지, 언제 어디에서 획득했는지, 어떤 센서와 소프트웨어 버전이 사용되었는지, 어떠한 운영 조건에서 생성되었는지를 파악할 수 있어야 한다. 출처 정보(Provenance)는 이후 검증과 디버깅(Debugging)을 가능하게 하며, 공유 지식이 신뢰성, 출처, 관련성을 확인할 수 없는 익명의 정보 집합으로 변하는 것을 방지한다.

서로 다른 관측은 신뢰성이 다를 수 있으므로 공유 지식에는 신뢰도(Confidence)가 함께 포함되어야 한다. 위치추정 성능이 저하되었거나 센서가 오염된 로봇의 정보는 높은 신뢰도의 인식을 수행하는 로봇의 정보와 동일한 수준으로 플릿 지식에 영향을 미쳐서는 안 된다. 따라서 공유 표현(Shared Representation)은 관측 정보와 함께 불확실성(Uncertainty), 신뢰도 점수, 품질 지표(Quality Indicator), 검증 상태(Validation Status)를 포함할 수 있다. 이에 따라 지식 융합(Knowledge Fusion)은 정보의 내용과 추정된 신뢰성을 함께 고려하여 증거를 결합하는 과정이 된다.

분산형 물리 시스템(Distributed Physical System)에서는 지식 충돌(Conflicting Knowledge)이 불가피하다. 두 로봇이 동일한 지형을 서로 다르게 분류하거나, 서로 다른 객체 위치를 보고하거나, 다른 시간에 동일한 환경을 관측할 수 있다. 이러한 불일치가 반드시 한 로봇의 오류를 의미하는 것은 아니며 관측 사이에 실제 물리 세계가 변화했을 수도 있다. 따라서 집단 시스템은 정보를 병합, 교체, 개별 유지하거나 불확실한 상태로 표시하기 전에 타임스탬프, 신뢰도, 맥락(Context), 센서 역량, 환경의 동적 특성을 비교해야 한다.

공유 경험은 성공(Success), 실패(Failure), 복구(Recovery)를 함께 포함할 때 특히 강력해진다. 성공적인 궤적만 기록하는 플릿은 정상적으로 작동하는 방법을 학습할 수 있지만 운영 한계에 대한 정보는 제한적이다. 실패 에피소드는 정책이 어떤 조건에서 제대로 작동하지 않는지를 보여주며, 복구 에피소드는 로봇이 어떻게 다시 안전하거나 생산적인 상태로 돌아갈 수 있는지를 보여준다. 이러한 경험을 함께 활용하면 더욱 강건한 내비게이션, 조작, 협조(Coordination), 자율 의사결정(Autonomous Decision Making)을 지원할 수 있다.

이기종 플릿(Heterogeneous Fleet)에서는 로봇마다 서로 다른 체화(Embodiment)와 역량을 가지기 때문에 지식 공유가 더욱 어려워진다. 자율이동로봇(AMR), 4족 보행 로봇(Quadruped), 매니퓰레이터(Manipulator), 휴머노이드(Humanoid), 무인항공기(UAV)의 경험은 센싱 공간과 행동 공간이 서로 다르기 때문에 항상 직접적으로 전이할 수 있는 것은 아니다. 그러나 객체, 위험, 작업 구조, 공간 관계, 의미론적 환경, 임무 결과와 같은 상위 수준의 지식은 플랫폼별 제어 명령과 독립적으로 표현할 경우 서로 다른 로봇 사이에서도 전이될 수 있다.

따라서 공유 지식은 공통 지식(Common Knowledge)과 로봇 특화 지식(Robot-Specific Knowledge)으로 구성할 수 있다. 공통 지식은 플릿 전체에서 광범위하게 활용할 수 있는 정보를 나타내며, 로봇 특화 지식은 체화, 센서 구성, 적재 능력, 이동성, 캘리브레이션, 운영 제약과 관련된 정보를 포함한다. 이러한 분리는 모든 로봇이 동일한 행동을 수행하거나 모든 관측을 정확히 동일한 방식으로 해석한다고 가정하지 않으면서도 다양한 경험을 집단 지능(Collective Intelligence)에 활용할 수 있도록 한다.

전체 과정은 지속적인 지식 생명주기(Knowledge Lifecycle)를 형성한다. 로봇은 물리적 운영 과정에서 경험을 생성하고, 가치 있는 관측을 선택하며, 맥락과 신뢰도 정보를 추가하여 공유 저장소(Shared Storage) 또는 분산 학습 메커니즘(Distributed Learning Mechanism)에 제공한다. 이후 플릿은 이러한 경험을 필터링, 통합, 검증하고 재사용 가능한 지식으로 변환하며, 생성된 지식을 다시 로봇에 배포하여 이후의 인식, 계획, 작업 실행, 학습 과정에서 활용하도록 한다.

따라서 공유 경험과 로봇 지식은 집단 학습을 가능하게 하는 정보적 기반(Informational Foundation)을 제공한다. 이는 개별 로봇의 물리적 상호작용과 플릿 규모 지능(Fleet-Scale Intelligence)을 연결하고, 중앙집중식 학습과 분산 실행(Centralized Training and Distributed Execution), 다중 에이전트 강화학습(Multi-Agent Reinforcement Learning), 연합 로봇 학습(Federated Robot Learning), 분산 모델 업데이트(Distributed Model Updates), 정책 및 기술 공유(Policy and Skill Sharing), 로봇 간 경험 재현(Cross-Robot Experience Replay), 전이학습(Transfer Learning)을 위한 기반을 마련한다. 배포 규모가 증가함에 따라 모든 로봇은 더 넓은 피지컬 AI 플릿(Physical AI Fleet)을 위한 지식의 소비자이자 생산자로 발전할 수 있다.

##  

## 05.03. Centralized Training and Distributed Execution

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

Centralized Training and Distributed Execution (CTDE) is a learning architecture designed to combine global information during training with autonomous local decision making during deployment. In a multi-robot Physical AI system, a centralized training process can access experiences collected across the fleet, while each deployed robot executes its learned policy using locally available observations, internal state, and permitted shared information.

The central motivation for CTDE is that training and execution operate under different information constraints. During training, historical trajectories from many robots can be aggregated without requiring every decision to satisfy real-time communication limits. The learning system can therefore examine relationships among robot states, actions, task outcomes, and environmental conditions that an individual robot cannot observe completely during physical operation.

Centralized training provides a broader view of collective behavior than isolated robot training. A trainer may observe joint states, actions, rewards, task assignments, communication events, and interactions among multiple robots. This additional context makes it possible to evaluate whether an individual action contributes to the overall mission rather than considering only its immediate local outcome, which is especially important when robots cooperate toward shared objectives.

Distributed execution removes dependence on a continuously available central intelligence during operation. Once training is completed, each robot receives a policy or model that can generate actions from information available at execution time. Navigation, manipulation, exploration, task execution, and local coordination can therefore continue even when communication with an on-premise or cloud training infrastructure becomes delayed, bandwidth-limited, intermittent, or temporarily unavailable.

This separation is particularly important for Physical AI because control decisions frequently have strict latency requirements. A robot cannot wait for a remote training server before reacting to a nearby person, avoiding an obstacle, stabilizing motion, or handling an unexpected physical event. Distributed execution keeps time-critical inference close to the robot, while computationally intensive learning and fleet-wide optimization can be performed using more powerful centralized computing resources.

A typical CTDE lifecycle begins with robots operating independently or cooperatively and generating trajectories containing observations, actions, rewards, task results, failures, and coordination events. Selected experiences are transferred to shared storage, where they can be synchronized, filtered, normalized, labeled, and associated with robot identity, environment, policy version, confidence, and other contextual metadata before being used for centralized learning.

The centralized learner can exploit joint experience to discover relationships that are difficult to identify from a single robot\'s history. For example, one robot\'s path choice may create congestion for another robot, or one agent\'s exploration behavior may reduce uncertainty for the entire team. Training with collective context enables the model to associate local decisions with their broader effects on throughput, safety, resource utilization, coverage, and mission success.

However, the policy deployed to a robot must respect the information available during execution. A model that requires the exact states of every fleet member during training may fail if those states are unavailable in the field. CTDE therefore requires careful separation between privileged training information and executable policy inputs. Global information can guide learning, but the resulting local policy must remain usable under realistic sensing and communication conditions.

One common approach is to use centralized value estimation together with decentralized policies. During training, a critic or value model can evaluate actions using information from multiple agents, while each robot\'s policy uses only its local observation or limited communication context. The centralized component helps estimate the consequences of coordinated behavior, whereas the distributed policies preserve autonomous execution after deployment.

CTDE can also improve the credit assignment problem in cooperative learning. When a team receives a shared reward, it may be unclear which robot or action caused success or failure. Access to joint trajectories during training provides additional evidence for identifying useful contributions and harmful interactions. This can help robots learn complementary behaviors rather than independently maximizing local objectives that may conflict with overall fleet performance.

Distributed execution does not necessarily mean that robots operate without communication. Robots may still exchange intent, task status, map updates, local observations, or coordination messages when connectivity is available. The essential principle is that execution should not require continuous centralized decision making. Communication becomes an operational resource that improves coordination rather than a mandatory dependency whose loss immediately prevents autonomous behavior.

Different robots can also receive different policies within the same CTDE architecture. In homogeneous fleets, parameter sharing may allow many robots to use a common policy, reducing training and deployment complexity. In heterogeneous fleets, AMRs, manipulators, quadrupeds, humanoids, and UAVs may require embodiment-specific policies while sharing centralized representations, objectives, critics, world knowledge, or training experience.

The architecture must also manage the transition between training and real-world deployment. Centralized models may be trained using richer information, large datasets, simulation, replay buffers, and fleet-wide statistics, but execution occurs under sensor noise, latency, partial observability, hardware variation, and environmental change. Evaluation must therefore verify that decentralized policies remain stable and effective when privileged training information is removed.

Continuous fleet learning extends CTDE beyond a single training cycle. Deployed robots generate new physical experience, which returns to the centralized learning infrastructure for analysis and model improvement. Updated policies are validated before controlled redistribution to the fleet. This creates a repeated sequence of distributed experience generation, centralized learning, verification, deployment, and renewed experience collection.

Safety and version management become critical as this cycle accelerates. A newly trained policy should not automatically replace every deployed policy simply because centralized evaluation reports improved average performance. Policies can be tested in simulation, replayed against difficult fleet episodes, evaluated on safety-critical scenarios, and gradually deployed to selected robots before wider rollout. Rollback mechanisms can restore previously validated versions if unexpected behavior appears.

CTDE therefore provides a practical bridge between fleet-scale collective intelligence and robot-level autonomy. Centralized training allows the system to learn from shared experience and global interactions, while distributed execution preserves responsiveness, scalability, and resilience in the physical world. Within collective learning, this architecture establishes an important foundation for multi-agent reinforcement learning, cooperative policy optimization, heterogeneous robot learning, and continuously improving Physical AI fleets.

중앙집중식 학습과 분산 실행(Centralized Training and Distributed Execution, CTDE)은 학습 과정에서는 전역 정보(Global Information)를 활용하면서 실제 배포 환경에서는 자율적인 로컬 의사결정(Local Decision Making)을 수행하도록 설계된 학습 아키텍처이다. 다중 로봇 피지컬 AI(Multi-Robot Physical AI) 시스템에서 중앙집중식 학습 과정은 전체 플릿(Fleet)에서 수집된 경험에 접근할 수 있으며, 배포된 각 로봇은 로컬에서 이용 가능한 관측(Observation), 내부 상태(Internal State), 허용된 공유 정보를 이용하여 학습된 정책(Policy)을 실행한다.

CTDE의 핵심적인 동기는 학습(Training)과 실행(Execution)이 서로 다른 정보 제약(Information Constraint) 아래에서 이루어진다는 점이다. 학습 과정에서는 모든 의사결정이 실시간 통신 제약을 충족할 필요 없이 여러 로봇의 과거 궤적(Trajectory)을 통합할 수 있다. 따라서 학습 시스템은 개별 로봇이 물리적 운영 과정에서 완전하게 관측할 수 없는 로봇 상태, 행동, 작업 결과, 환경 조건 사이의 관계를 분석할 수 있다.

중앙집중식 학습(Centralized Training)은 개별 로봇 학습보다 집단 행동(Collective Behavior)을 더욱 폭넓게 파악할 수 있도록 한다. 학습 시스템은 여러 로봇의 공동 상태(Joint State), 행동, 보상(Reward), 작업 할당(Task Assignment), 통신 이벤트, 로봇 간 상호작용을 관측할 수 있다. 이러한 추가적인 맥락(Context)을 이용하면 개별 행동의 즉각적인 로컬 결과만 고려하는 것이 아니라 해당 행동이 전체 임무에 기여하는지를 평가할 수 있으며, 이는 로봇들이 공동 목표를 위해 협력할 때 특히 중요하다.

분산 실행(Distributed Execution)은 실제 운영 과정에서 지속적으로 사용 가능한 중앙 지능(Central Intelligence)에 대한 의존성을 제거한다. 학습이 완료되면 각 로봇은 실행 시 이용할 수 있는 정보를 바탕으로 행동을 생성하는 정책이나 모델을 전달받는다. 따라서 온프레미스(On-Premise) 또는 클라우드(Cloud) 학습 인프라와의 통신이 지연되거나, 대역폭이 제한되거나, 간헐적으로 끊기거나, 일시적으로 사용할 수 없는 상황에서도 내비게이션, 조작, 탐색, 작업 실행, 로컬 협조(Local Coordination)를 계속 수행할 수 있다.

이러한 분리는 제어 의사결정(Control Decision)에 엄격한 지연시간 요구사항(Latency Requirement)이 존재하는 피지컬 AI(Physical AI)에서 특히 중요하다. 로봇은 주변 사람에게 반응하거나 장애물을 회피하고, 움직임을 안정화하거나 예상하지 못한 물리적 사건에 대응하기 위해 원격 학습 서버의 응답을 기다릴 수 없다. 분산 실행은 시간에 민감한 추론(Time-Critical Inference)을 로봇 가까이에서 수행하게 하며, 계산량이 많은 학습과 플릿 전체 최적화는 더욱 강력한 중앙집중식 컴퓨팅 자원을 이용하여 수행할 수 있도록 한다.

일반적인 CTDE 생명주기(Lifecycle)는 로봇들이 독립적으로 또는 협력적으로 운영되면서 관측, 행동, 보상, 작업 결과, 실패, 협조 이벤트(Coordination Event)를 포함하는 궤적을 생성하는 것에서 시작한다. 선택된 경험은 공유 저장소(Shared Storage)로 전송되고, 중앙집중식 학습에 사용되기 전에 동기화, 필터링, 정규화, 라벨링되며 로봇 식별정보, 환경, 정책 버전, 신뢰도(Confidence), 기타 맥락 메타데이터(Contextual Metadata)와 연결될 수 있다.

중앙집중식 학습기(Centralized Learner)는 공동 경험(Joint Experience)을 활용하여 단일 로봇의 이력만으로는 파악하기 어려운 관계를 발견할 수 있다. 예를 들어 한 로봇의 경로 선택이 다른 로봇의 혼잡을 발생시키거나, 하나의 에이전트가 수행한 탐색 행동이 전체 팀의 불확실성(Uncertainty)을 감소시킬 수 있다. 집단 맥락을 활용한 학습은 로컬 의사결정이 처리량(Throughput), 안전성, 자원 활용, 탐색 범위(Coverage), 임무 성공에 미치는 광범위한 영향을 모델이 학습하도록 한다.

그러나 로봇에 배포되는 정책은 실행 시 실제로 이용 가능한 정보의 범위를 준수해야 한다. 학습 과정에서 전체 플릿 구성원의 정확한 상태를 요구하는 모델은 현장에서 이러한 정보를 이용할 수 없을 경우 제대로 동작하지 않을 수 있다. 따라서 CTDE에서는 특권 학습 정보(Privileged Training Information)와 실행 가능한 정책 입력(Executable Policy Input)을 명확하게 분리해야 한다. 전역 정보는 학습을 지원할 수 있지만 최종적인 로컬 정책은 현실적인 센싱과 통신 조건에서도 실행 가능해야 한다.

일반적인 접근 방법 가운데 하나는 중앙집중식 가치 추정(Centralized Value Estimation)과 분산 정책(Decentralized Policy)을 함께 사용하는 것이다. 학습 과정에서 크리틱(Critic) 또는 가치 모델(Value Model)은 여러 에이전트의 정보를 이용하여 행동을 평가할 수 있지만, 각 로봇의 정책은 자신의 로컬 관측이나 제한된 통신 맥락만을 이용한다. 중앙집중식 구성요소는 협력 행동의 결과를 평가하는 데 도움을 주고, 분산 정책은 배포 이후에도 자율적인 실행을 유지하도록 한다.

CTDE는 협력 학습(Cooperative Learning)에서의 기여도 할당 문제(Credit Assignment Problem)를 개선할 수도 있다. 팀 전체가 하나의 공유 보상을 받는 경우 어떤 로봇 또는 어떤 행동이 성공이나 실패의 원인이 되었는지를 판단하기 어려울 수 있다. 학습 과정에서 공동 궤적(Joint Trajectory)에 접근하면 유용한 기여와 해로운 상호작용을 식별하기 위한 추가적인 근거를 확보할 수 있다. 이를 통해 로봇은 전체 플릿 성능과 충돌할 수 있는 개별 목표만을 독립적으로 극대화하는 대신 서로 보완적인 행동을 학습할 수 있다.

분산 실행이 반드시 로봇들이 통신 없이 동작한다는 것을 의미하지는 않는다. 연결이 가능한 경우 로봇은 의도(Intent), 작업 상태, 지도 업데이트, 로컬 관측, 협조 메시지를 계속 교환할 수 있다. 핵심 원리는 실행이 지속적인 중앙집중식 의사결정에 의존하지 않아야 한다는 것이다. 통신은 자율 행동을 유지하기 위한 필수적인 단일 의존성이 아니라 협조 성능을 향상시키는 운영 자원(Operational Resource)이 된다.

동일한 CTDE 아키텍처 내에서도 서로 다른 로봇에 서로 다른 정책을 제공할 수 있다. 동종 플릿(Homogeneous Fleet)에서는 파라미터 공유(Parameter Sharing)를 통해 다수의 로봇이 공통 정책을 사용함으로써 학습과 배포의 복잡성을 줄일 수 있다. 이기종 플릿(Heterogeneous Fleet)에서는 자율이동로봇(AMR), 매니퓰레이터(Manipulator), 4족 보행 로봇(Quadruped), 휴머노이드(Humanoid), 무인항공기(UAV)가 서로 다른 체화 특화 정책(Embodiment-Specific Policy)을 사용하면서 중앙집중식 표현, 목표, 크리틱, 세계 지식(World Knowledge), 학습 경험을 공유할 수 있다.

이 아키텍처는 학습에서 실제 환경 배포(Real-World Deployment)로 전환되는 과정도 관리해야 한다. 중앙집중식 모델은 더욱 풍부한 정보, 대규모 데이터셋, 시뮬레이션(Simulation), 리플레이 버퍼(Replay Buffer), 플릿 전체 통계를 이용하여 학습할 수 있지만, 실제 실행은 센서 노이즈, 지연시간, 부분 관측 가능성(Partial Observability), 하드웨어 편차, 환경 변화가 존재하는 조건에서 이루어진다. 따라서 평가 과정에서는 특권 학습 정보가 제거된 상황에서도 분산 정책이 안정적이고 효과적으로 동작하는지를 검증해야 한다.

지속적인 플릿 학습(Continuous Fleet Learning)은 CTDE를 단일 학습 주기를 넘어 지속적인 과정으로 확장한다. 배포된 로봇은 새로운 물리적 경험을 생성하고, 이러한 경험은 분석과 모델 개선을 위해 중앙집중식 학습 인프라로 다시 전달된다. 업데이트된 정책은 검증된 이후 통제된 방식으로 플릿에 재배포된다. 이를 통해 분산 경험 생성(Distributed Experience Generation), 중앙집중식 학습, 검증(Verification), 배포, 새로운 경험 수집으로 이어지는 반복적인 순환 구조가 형성된다.

이러한 순환이 빨라질수록 안전(Safety)과 버전 관리(Version Management)는 더욱 중요해진다. 중앙집중식 평가에서 평균 성능이 향상되었다는 이유만으로 새롭게 학습된 정책이 모든 로봇의 기존 정책을 자동으로 교체해서는 안 된다. 정책은 시뮬레이션에서 시험하고, 어려운 플릿 에피소드를 이용하여 재현 평가하며, 안전 중요 시나리오(Safety-Critical Scenario)에서 검증한 후 일부 로봇에 단계적으로 배포할 수 있다. 예상하지 못한 행동이 발생하면 롤백 메커니즘(Rollback Mechanism)을 통해 이전에 검증된 버전으로 복구할 수 있다.

따라서 CTDE는 플릿 규모 집단 지능(Fleet-Scale Collective Intelligence)과 로봇 수준 자율성(Robot-Level Autonomy)을 연결하는 실용적인 구조를 제공한다. 중앙집중식 학습은 공유 경험과 전역 상호작용으로부터 시스템이 학습하도록 하며, 분산 실행은 물리적 세계에서 반응성(Responsiveness), 확장성(Scalability), 회복탄력성(Resilience)을 유지하도록 한다. 집단 학습(Collective Learning)에서 이러한 아키텍처는 다중 에이전트 강화학습(Multi-Agent Reinforcement Learning), 협력 정책 최적화(Cooperative Policy Optimization), 이기종 로봇 학습(Heterogeneous Robot Learning), 지속적으로 개선되는 피지컬 AI 플릿을 위한 중요한 기반을 형성한다.

##  

## 05.04. Multi Agent Reinforcement Learning

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

Multi-Agent Reinforcement Learning (MARL) extends reinforcement learning from a single decision-making agent to multiple agents that learn while interacting within the same environment. In multi-robot Physical AI, each robot selects physical actions according to its observations and policy, while the resulting rewards and state transitions may depend on the simultaneous behavior of other robots. Learning therefore becomes a problem of both individual adaptation and collective interaction.

Unlike single-agent reinforcement learning, MARL introduces other learning agents into the effective environment of each robot. As their policies change during training, the transition and reward patterns observed by any individual robot also change. This creates non-stationarity, because a behavior that produced a useful result under one set of teammate policies may produce a different outcome after those policies have been updated.

MARL problems can be cooperative, competitive, or mixed, but collective robot learning commonly emphasizes cooperative objectives. Robots may share a global reward associated with mission completion, throughput, coverage, energy efficiency, safety, or task success. The learning process must then discover policies that produce useful joint behavior rather than merely improving the immediate performance of each robot independently.

Partial observability is another fundamental challenge. A physical robot normally observes only a limited region through its onboard sensors and cannot directly access the complete state of the environment or every teammate. Its decisions must therefore be based on local observations, internal memory, shared messages, or estimated team context. Effective MARL policies must learn useful behavior despite incomplete and potentially delayed information.

The joint action space grows rapidly as the number of robots increases. If every robot has several possible actions, the number of possible joint action combinations can become extremely large even for a moderate fleet. This combinatorial growth makes direct optimization difficult and motivates scalable approaches based on parameter sharing, factorized value functions, hierarchical policies, local interaction structures, or centralized training with decentralized execution.

Centralized Training and Distributed Execution (CTDE) is especially relevant to MARL because it provides richer information during learning without requiring centralized control during deployment. A centralized critic may observe joint states, actions, rewards, or team context while evaluating behavior, whereas each robot maintains an actor or policy that operates from locally available information. This structure supports coordinated learning while preserving physical autonomy.

Reward design strongly influences the collective behavior that emerges. Purely individual rewards may encourage robots to compete for resources or select locally efficient actions that reduce fleet-level performance. A purely global reward can encourage cooperation but may make it difficult to determine which robot contributed to an outcome. Practical MARL systems often balance individual, team, safety, and task-specific reward components to shape desirable behavior.

This leads directly to the credit assignment problem. When several robots cooperate and receive a shared reward, the learner must estimate how individual actions contributed to collective success or failure. For example, a robot that temporarily takes a longer route may reduce congestion and improve total fleet throughput even though its own travel time increases. Effective credit assignment allows learning to recognize such indirectly beneficial actions.

Communication can become part of the learned coordination process. Robots may exchange positions, intentions, task status, map information, uncertainty, or compact latent messages. In more advanced approaches, the system can learn what information should be communicated, when communication is valuable, and which teammates should receive it. Communication-aware MARL is particularly useful when bandwidth and connectivity are limited operational resources.

MARL can also support specialization and complementary roles. Instead of learning identical behavior, robots may discover policies that divide responsibilities according to position, capability, task demand, or embodiment. One robot may explore while another transports material, observes a hazardous area, relays communication, or performs manipulation. Collective reward encourages these different behaviors when their combination improves the overall mission outcome.

Heterogeneous robots make this problem more complex because their observation spaces, action spaces, dynamics, and physical capabilities may differ significantly. An AMR cannot execute the same actions as a UAV or manipulator, yet all may participate in one mission. MARL architectures for heterogeneous fleets can combine embodiment-specific policies with shared representations, team objectives, centralized critics, or common task-level abstractions.

Training MARL policies directly on physical robots is expensive and potentially unsafe because effective reinforcement learning can require large numbers of interactions and exploratory actions. Simulation therefore plays an important role in generating parallel multi-agent experience. Large numbers of virtual robots can explore coordination strategies, congestion situations, task assignments, communication failures, and recovery scenarios before policies are transferred and validated in real systems.

Simulation alone is insufficient because real robots encounter sensor noise, actuator variation, communication delay, localization errors, friction changes, human behavior, and unexpected environmental conditions. Policies intended for physical deployment must therefore be evaluated under disturbances and uncertainty. Domain randomization, realistic communication models, hardware-aware dynamics, safety constraints, and controlled real-world fine-tuning can reduce the gap between simulated collective behavior and actual fleet operation.

Experience replay across robots can improve data efficiency by allowing trajectories generated by different agents to contribute to subsequent learning. However, replay data may have been collected under older policies, making it increasingly inconsistent with the current behavior of the fleet. Policy version information, recency weighting, prioritized sampling, and careful replay management help prevent outdated experience from destabilizing multi-agent learning.

Safety constraints must remain explicit because exploration in MARL affects not only one robot but potentially an entire physical team. Collision avoidance, restricted areas, human safety, actuator limits, communication loss behavior, and emergency fallback policies should not depend solely on learned rewards. Runtime assurance and conventional safety mechanisms can operate alongside learned policies to constrain unsafe actions during both experimentation and deployment.

At fleet scale, MARL provides a mechanism through which repeated local interactions can produce coordinated collective policies. Robots generate distributed experience, centralized or distributed learners extract patterns from joint outcomes, and improved policies return to the fleet for further execution. This feedback cycle connects reinforcement learning with shared experience, CTDE, policy sharing, experience replay, transfer learning, and continual fleet adaptation.

Multi-Agent Reinforcement Learning therefore provides a core learning framework for robots whose performance depends on the behavior of other robots. Its central challenge is not simply to make many individual agents intelligent, but to learn policies whose interactions produce effective collective behavior under partial observability, limited communication, heterogeneous embodiment, and physical uncertainty. In collective Physical AI, MARL turns repeated multi-robot interaction into progressively improved coordination and team intelligence.

다중 에이전트 강화학습(Multi-Agent Reinforcement Learning, MARL)은 강화학습(Reinforcement Learning)을 하나의 의사결정 에이전트에서 동일한 환경 안에서 상호작용하며 학습하는 여러 에이전트로 확장한 것이다. 다중 로봇 피지컬 AI(Multi-Robot Physical AI)에서 각 로봇은 자신의 관측과 정책(Policy)에 따라 물리적 행동을 선택하며, 그 결과로 얻는 보상(Reward)과 상태 전이(State Transition)는 다른 로봇의 동시 행동에 따라 달라질 수 있다. 따라서 학습은 개별 적응(Individual Adaptation)과 집단 상호작용(Collective Interaction)을 동시에 다루는 문제가 된다.

단일 에이전트 강화학습(Single-Agent Reinforcement Learning)과 달리 MARL에서는 다른 학습 에이전트들이 각 로봇이 경험하는 실질적인 환경의 일부가 된다. 학습 과정에서 다른 에이전트들의 정책이 변화하면 개별 로봇이 관측하는 상태 전이와 보상 패턴도 함께 변화한다. 이로 인해 비정상성(Non-Stationarity)이 발생하며, 특정 팀원 정책에서 유용한 결과를 만들었던 행동이 해당 정책이 업데이트된 이후에는 다른 결과를 만들어낼 수 있다.

MARL 문제는 협력적(Cooperative), 경쟁적(Competitive), 혼합형(Mixed)으로 구성할 수 있지만, 집단 로봇 학습(Collective Robot Learning)에서는 일반적으로 협력적 목표를 중요하게 다룬다. 로봇들은 임무 완료, 처리량(Throughput), 커버리지(Coverage), 에너지 효율, 안전, 작업 성공과 관련된 전역 보상(Global Reward)을 공유할 수 있다. 학습 과정은 각 로봇의 즉각적인 성능만 독립적으로 향상시키는 것이 아니라 유용한 공동 행동(Joint Behavior)을 만들어내는 정책을 발견해야 한다.

부분 관측 가능성(Partial Observability)은 또 다른 근본적인 문제이다. 물리적 로봇은 일반적으로 온보드 센서(Onboard Sensor)를 통해 제한된 영역만 관측하며, 환경 전체의 상태나 모든 팀원의 상태에 직접 접근할 수 없다. 따라서 로봇은 로컬 관측(Local Observation), 내부 메모리(Internal Memory), 공유 메시지(Shared Message), 추정된 팀 맥락(Team Context)을 기반으로 의사결정을 수행해야 한다. 효과적인 MARL 정책은 불완전하고 지연될 가능성이 있는 정보에서도 유용한 행동을 학습해야 한다.

로봇의 수가 증가할수록 공동 행동 공간(Joint Action Space)은 빠르게 증가한다. 각 로봇이 여러 개의 가능한 행동을 가진다면 중간 규모의 플릿에서도 가능한 공동 행동 조합의 수가 매우 커질 수 있다. 이러한 조합적 증가(Combinatorial Growth)는 직접적인 최적화를 어렵게 만들며, 파라미터 공유(Parameter Sharing), 분해된 가치 함수(Factorized Value Function), 계층적 정책(Hierarchical Policy), 로컬 상호작용 구조(Local Interaction Structure), 중앙집중식 학습과 분산 실행(Centralized Training with Decentralized Execution)과 같은 확장 가능한 접근법을 필요로 한다.

중앙집중식 학습과 분산 실행(Centralized Training and Distributed Execution, CTDE)은 배포 과정에서 중앙집중식 제어를 요구하지 않으면서 학습 과정에서는 더욱 풍부한 정보를 제공하기 때문에 MARL에서 특히 중요하다. 중앙집중식 크리틱(Centralized Critic)은 행동을 평가할 때 공동 상태, 행동, 보상, 팀 맥락을 관측할 수 있는 반면, 각 로봇은 로컬에서 이용 가능한 정보만으로 동작하는 액터(Actor) 또는 정책을 유지한다. 이러한 구조는 물리적 자율성을 유지하면서 협력적인 학습을 가능하게 한다.

보상 설계(Reward Design)는 어떠한 집단 행동이 출현하는지를 크게 좌우한다. 순수하게 개별적인 보상은 로봇들이 자원을 두고 경쟁하거나 플릿 전체의 성능을 감소시키면서도 로컬에서는 효율적인 행동을 선택하도록 만들 수 있다. 반대로 순수한 전역 보상은 협력을 촉진하지만 어떤 로봇이 특정 결과에 기여했는지 판단하기 어렵게 만들 수 있다. 실제 MARL 시스템에서는 바람직한 행동을 유도하기 위해 개별, 팀, 안전, 작업 특화 보상 요소를 적절하게 조합하는 경우가 많다.

이는 기여도 할당 문제(Credit Assignment Problem)로 직접 연결된다. 여러 로봇이 협력하면서 공유 보상을 받을 경우 학습 시스템은 각각의 행동이 집단의 성공이나 실패에 어떻게 기여했는지를 추정해야 한다. 예를 들어 한 로봇이 일시적으로 더 긴 경로를 선택하면 자신의 이동 시간은 증가하지만 혼잡을 줄여 전체 플릿 처리량을 향상시킬 수 있다. 효과적인 기여도 할당은 이러한 간접적으로 유익한 행동까지 학습 과정에서 인식할 수 있도록 한다.

통신(Communication)은 학습되는 협조 과정(Learned Coordination Process)의 일부가 될 수도 있다. 로봇은 위치, 의도(Intent), 작업 상태, 지도 정보, 불확실성 또는 압축된 잠재 메시지(Latent Message)를 교환할 수 있다. 더욱 발전된 접근법에서는 어떤 정보를 통신해야 하는지, 언제 통신이 가치가 있는지, 어떤 팀원에게 정보를 전달해야 하는지까지 학습할 수 있다. 통신 인식 MARL(Communication-Aware MARL)은 대역폭과 연결성이 제한된 운영 자원인 환경에서 특히 유용하다.

MARL은 전문화(Specialization)와 상호보완적 역할(Complementary Role)의 형성도 지원할 수 있다. 모든 로봇이 동일한 행동을 학습하는 대신 위치, 역량, 작업 요구사항 또는 체화(Embodiment)에 따라 책임을 분담하는 정책을 발견할 수 있다. 하나의 로봇이 탐색을 수행하는 동안 다른 로봇은 물자를 운반하거나, 위험 지역을 관측하거나, 통신을 중계하거나, 조작 작업을 수행할 수 있다. 이러한 서로 다른 행동의 조합이 전체 임무 성과를 개선한다면 집단 보상은 역할 분화를 촉진할 수 있다.

이기종 로봇(Heterogeneous Robots)은 관측 공간(Observation Space), 행동 공간(Action Space), 동역학(Dynamics), 물리적 역량이 크게 다를 수 있기 때문에 문제를 더욱 복잡하게 만든다. 자율이동로봇(AMR)은 무인항공기(UAV)나 매니퓰레이터(Manipulator)와 동일한 행동을 실행할 수 없지만 하나의 임무에 함께 참여할 수 있다. 이기종 플릿을 위한 MARL 아키텍처는 체화 특화 정책(Embodiment-Specific Policy)을 공유 표현, 팀 목표, 중앙집중식 크리틱, 공통 작업 수준 추상화(Common Task-Level Abstraction)와 결합할 수 있다.

MARL 정책을 실제 물리적 로봇에서 직접 학습하는 것은 효과적인 강화학습에 많은 상호작용과 탐색 행동이 필요할 수 있기 때문에 비용이 많이 들고 잠재적으로 위험하다. 따라서 시뮬레이션(Simulation)은 병렬적인 다중 에이전트 경험을 생성하는 데 중요한 역할을 한다. 많은 수의 가상 로봇이 실제 시스템으로 정책을 전이하고 검증하기 전에 협조 전략, 혼잡 상황, 작업 할당, 통신 실패, 복구 시나리오를 탐색할 수 있다.

그러나 실제 로봇은 센서 노이즈, 액추에이터 편차(Actuator Variation), 통신 지연, 위치추정 오류, 마찰 변화, 인간 행동, 예상하지 못한 환경 조건을 경험하기 때문에 시뮬레이션만으로는 충분하지 않다. 따라서 물리적 배포를 위한 정책은 교란(Disturbance)과 불확실성이 존재하는 조건에서 평가되어야 한다. 도메인 랜덤화(Domain Randomization), 현실적인 통신 모델, 하드웨어 인식 동역학(Hardware-Aware Dynamics), 안전 제약, 통제된 실제 환경 미세조정(Real-World Fine-Tuning)은 시뮬레이션의 집단 행동과 실제 플릿 운영 사이의 차이를 줄이는 데 활용할 수 있다.

로봇 간 경험 재현(Experience Replay Across Robots)은 서로 다른 에이전트가 생성한 궤적을 이후의 학습에 활용함으로써 데이터 효율성을 향상시킬 수 있다. 그러나 리플레이 데이터(Replay Data)는 이전 정책에서 수집되었을 가능성이 있으며, 시간이 지날수록 현재 플릿의 행동과 일치하지 않을 수 있다. 정책 버전 정보(Policy Version Information), 최신성 가중치(Recency Weighting), 우선순위 샘플링(Prioritized Sampling), 적절한 리플레이 관리는 오래된 경험으로 인해 다중 에이전트 학습이 불안정해지는 것을 방지하는 데 도움을 준다.

MARL에서의 탐색은 하나의 로봇뿐만 아니라 물리적으로 동작하는 전체 팀에 영향을 줄 수 있으므로 안전 제약(Safety Constraint)을 명시적으로 유지해야 한다. 충돌 회피, 제한 구역, 인간 안전, 액추에이터 한계, 통신 손실 시 행동, 비상 폴백 정책(Emergency Fallback Policy)은 학습된 보상에만 의존해서는 안 된다. 런타임 보증(Runtime Assurance)과 기존 안전 메커니즘은 학습 정책과 함께 동작하면서 실험과 실제 배포 과정에서 위험한 행동을 제한할 수 있다.

플릿 규모(Fleet Scale)에서 MARL은 반복적인 로컬 상호작용으로부터 협력적인 집단 정책(Collective Policy)을 형성하는 메커니즘을 제공한다. 로봇들은 분산된 경험을 생성하고, 중앙집중식 또는 분산형 학습기(Distributed Learner)는 공동 결과에서 패턴을 추출하며, 개선된 정책은 추가적인 실행을 위해 다시 플릿에 전달된다. 이러한 피드백 순환은 강화학습을 공유 경험(Shared Experience), CTDE, 정책 공유(Policy Sharing), 경험 재현, 전이학습(Transfer Learning), 지속적인 플릿 적응(Continual Fleet Adaptation)과 연결한다.

따라서 다중 에이전트 강화학습(Multi-Agent Reinforcement Learning)은 다른 로봇의 행동에 따라 자신의 성능이 달라지는 로봇들을 위한 핵심 학습 프레임워크를 제공한다. 중심적인 과제는 단순히 여러 개별 에이전트를 지능적으로 만드는 것이 아니라 부분 관측 가능성, 제한된 통신, 이기종 체화(Heterogeneous Embodiment), 물리적 불확실성 아래에서도 효과적인 집단 행동을 만들어내는 정책을 학습하는 것이다. 집단 피지컬 AI(Collective Physical AI)에서 MARL은 반복적인 다중 로봇 상호작용을 점진적으로 향상되는 협조 능력과 팀 지능(Team Intelligence)으로 변환한다.

##  

## 05.05. Cooperative Imitation Learning

![](images/image6.png){width="7.268055555555556in" height="7.268055555555556in"}

Cooperative imitation learning extends imitation learning from a single robot copying demonstrations to multiple robots learning behaviors that depend on coordinated actions. Instead of asking only how one robot should reproduce an expert trajectory, the learning problem asks how several embodied agents should divide roles, synchronize actions, and respond to one another so that the team can reproduce successful collective behavior.

The demonstrations used for cooperative learning may come from humans, teleoperators, scripted controllers, expert robot teams, simulation, or previously validated fleet policies. A demonstration can contain synchronized observations, actions, task states, communication events, and outcomes from several agents. Preserving these relationships is important because the meaning of one robot\'s action may depend strongly on what other robots are doing at the same moment.

Consider a cooperative transport task in which two mobile robots move a large object together. Observing the trajectory of either robot independently provides only part of the required behavior. The useful demonstration includes their relative positions, timing, velocities, forces, path choices, and reactions to each other. Cooperative imitation learning attempts to capture this joint structure so that coordinated behavior can be reproduced rather than merely copying isolated motions.

A central challenge is deciding what information should be imitated. Low-level motor commands may reproduce demonstrations accurately but transfer poorly across robots, environments, or hardware configurations. Higher-level representations such as goals, roles, waypoints, relative formations, task phases, object states, or coordination intentions can provide greater flexibility. Practical systems may combine high-level shared behavior with embodiment-specific low-level controllers.

Behavior cloning provides a straightforward starting point. Demonstrated observation-action pairs are collected and policies are trained to predict expert actions from available observations. In cooperative settings, however, the training data must represent interactions among agents. A robot may need to condition its action not only on its own sensory input but also on teammate state, shared task context, communication, or inferred intent.

Pure behavior cloning can suffer from distribution shift. Small execution errors may move robots into states that were rarely represented in demonstrations, after which prediction errors accumulate. This problem can become more severe in multi-robot systems because one robot\'s deviation changes the conditions experienced by others. Interactive data collection, corrective demonstrations, recovery examples, and reinforcement learning can therefore complement imitation.

Role representation is especially important when demonstrations involve complementary behaviors. A warehouse team may include robots that transport goods, reposition containers, inspect aisles, or support manipulation. Cooperative imitation learning can associate actions with explicit roles or infer role structure from repeated demonstrations. Policies can then reproduce not only individual skills but also patterns of responsibility that make the overall team effective.

Communication may also be part of the demonstrated behavior. Expert teams can reveal when robots should share position, intent, task status, uncertainty, or requests for assistance. A learning system may imitate explicit communication actions or infer latent coordination signals from behavior. This enables robots to learn communication as a functional component of cooperation rather than treating message exchange as an independently engineered mechanism.

Temporal synchronization creates another challenge. Cooperative tasks frequently require actions to occur in a particular sequence or within a limited time relationship. One robot may need to wait until another reaches a location, holds an object, clears a passage, or completes an inspection. Demonstrations therefore contain temporal structure that should be preserved through task phases, event dependencies, recurrent memory, or other sequence-aware representations.

Cooperative demonstrations can also provide valuable examples of recovery. Expert operators often respond to blocked paths, failed grasps, communication delays, localization errors, or unexpected human activity with behaviors that are difficult to specify manually. Capturing these episodes allows the learning system to imitate not only nominal cooperation but also how a team reorganizes its behavior when normal execution is disrupted.

Shared experience increases the amount and diversity of demonstration data available to the fleet. Successful behaviors learned or demonstrated on one subset of robots can be stored, evaluated, and reused for others. Repeated demonstrations from different environments help distinguish essential coordination patterns from incidental details. The resulting dataset can gradually become a fleet-scale library of cooperative tasks, skills, recoveries, and interaction strategies.

Heterogeneous fleets require careful transfer because different embodiments cannot necessarily imitate the same physical action. An AMR, quadruped, UAV, manipulator, and humanoid have different mobility, sensing, dynamics, and action spaces. Cooperative imitation can instead transfer task-level concepts such as explore, observe, transport, support, relay, or manipulate while allowing each embodiment to realize the assigned behavior through its own controller and capabilities.

Centralized training and distributed execution can support cooperative imitation learning. During training, synchronized demonstrations from multiple robots can provide global context about team behavior, roles, interactions, and outcomes. During execution, each robot can use a decentralized policy based on locally available observations and permitted communication. The training system therefore benefits from rich demonstrations without requiring permanent centralized control.

Imitation learning and multi-agent reinforcement learning can also complement each other. Demonstrations provide a useful initial policy and reduce the amount of unsafe or inefficient exploration required from physical robots. Reinforcement learning can subsequently refine the imitated policy, adapt it to conditions not covered by demonstrations, and optimize collective objectives. This combination is attractive when expert examples are available but cannot cover every operational situation.

Demonstration quality remains critical because imitation reproduces systematic weaknesses as well as useful expertise. Inconsistent operators, inefficient coordination, unsafe shortcuts, or poorly synchronized demonstrations can introduce undesirable behavior. Fleet learning pipelines should therefore track demonstration provenance, evaluate outcomes, filter low-quality episodes, preserve safety constraints, and assign confidence or quality measures before incorporating demonstrations into shared training data.

Safety is particularly important when learned coordination involves physical interaction among robots or with humans. An imitated action should not automatically be accepted merely because it appeared in expert data. Collision constraints, separation requirements, actuator limits, restricted areas, human safety rules, and runtime assurance can remain independent of the learned policy. This allows imitation to improve behavior while established safety mechanisms constrain unacceptable actions.

Cooperative imitation learning ultimately provides a mechanism for converting successful team behavior into reusable fleet knowledge. Demonstrations capture how robots coordinate, specialize, communicate, synchronize, and recover, while learning transforms these examples into policies and skills that can be redistributed across the fleet. Within collective learning, it connects shared experience with policy sharing, cross-robot transfer, continual learning, and increasingly capable multi-robot Physical AI systems.

협력적 모방학습(Cooperative Imitation Learning)은 하나의 로봇이 시연(Demonstration)을 모방하는 기존 모방학습(Imitation Learning)을 여러 로봇이 협조된 행동(Coordinated Action)에 의존하는 행동을 학습하는 형태로 확장한다. 단순히 하나의 로봇이 전문가 궤적(Expert Trajectory)을 어떻게 재현할 것인가를 학습하는 것이 아니라, 여러 체화된 에이전트(Embodied Agent)가 역할을 분담하고 행동을 동기화하며 서로에게 반응함으로써 성공적인 집단 행동(Collective Behavior)을 재현하는 방법을 학습한다.

협력 학습(Cooperative Learning)에 사용되는 시연은 인간, 원격조작자(Teleoperator), 스크립트 기반 제어기(Scripted Controller), 전문가 로봇 팀, 시뮬레이션(Simulation), 또는 이전에 검증된 플릿 정책(Fleet Policy)으로부터 얻을 수 있다. 하나의 시연에는 여러 에이전트의 동기화된 관측(Observation), 행동(Action), 작업 상태(Task State), 통신 이벤트, 결과가 포함될 수 있다. 한 로봇의 행동 의미는 동일한 순간에 다른 로봇들이 무엇을 수행하는지에 크게 좌우될 수 있으므로 이러한 관계를 보존하는 것이 중요하다.

두 대의 이동 로봇이 하나의 대형 물체를 함께 운반하는 협력 운송 작업(Cooperative Transport Task)을 생각할 수 있다. 어느 한 로봇의 궤적만 관측해서는 필요한 행동의 일부만 파악할 수 있다. 유용한 시연에는 두 로봇의 상대 위치, 타이밍, 속도, 힘, 경로 선택, 상호 반응이 함께 포함된다. 협력적 모방학습은 고립된 움직임만 복제하는 것이 아니라 이러한 공동 구조(Joint Structure)를 학습하여 협조된 행동 자체를 재현하려 한다.

핵심적인 과제 가운데 하나는 어떤 정보를 모방해야 하는지를 결정하는 것이다. 저수준 모터 명령(Low-Level Motor Command)은 시연을 정확하게 재현할 수 있지만 서로 다른 로봇, 환경, 하드웨어 구성으로의 전이 성능이 낮을 수 있다. 목표, 역할, 경유점(Waypoint), 상대 대형(Relative Formation), 작업 단계(Task Phase), 객체 상태, 협조 의도(Coordination Intent)와 같은 상위 수준 표현은 더 높은 유연성을 제공할 수 있다. 실제 시스템에서는 상위 수준의 공유 행동과 체화 특화 저수준 제어기(Embodiment-Specific Low-Level Controller)를 결합할 수 있다.

행동 복제(Behavior Cloning)는 비교적 직접적인 출발점을 제공한다. 시연된 관측-행동 쌍(Observation-Action Pair)을 수집하고 이용 가능한 관측으로부터 전문가 행동을 예측하도록 정책(Policy)을 학습한다. 그러나 협력 환경에서는 학습 데이터가 에이전트 사이의 상호작용을 표현해야 한다. 로봇은 자신의 센서 입력뿐만 아니라 팀원의 상태, 공유 작업 맥락(Shared Task Context), 통신 정보 또는 추정된 의도(Inferred Intent)를 조건으로 행동을 결정해야 할 수 있다.

순수한 행동 복제는 분포 이동(Distribution Shift)의 영향을 받을 수 있다. 실행 과정에서 발생한 작은 오차로 인해 로봇이 시연 데이터에 거의 존재하지 않았던 상태로 이동하면 이후 예측 오차가 누적될 수 있다. 다중 로봇 시스템에서는 한 로봇의 편차가 다른 로봇이 경험하는 조건까지 변화시키므로 이러한 문제가 더욱 심각해질 수 있다. 따라서 상호작용형 데이터 수집(Interactive Data Collection), 교정 시연(Corrective Demonstration), 복구 사례, 강화학습(Reinforcement Learning)을 모방학습과 결합할 수 있다.

시연이 상호보완적인 행동(Complementary Behavior)을 포함하는 경우 역할 표현(Role Representation)은 특히 중요하다. 창고 로봇 팀에는 물품 운송, 컨테이너 재배치, 통로 검사, 조작 지원과 같은 서로 다른 역할이 존재할 수 있다. 협력적 모방학습은 행동을 명시적인 역할과 연결하거나 반복되는 시연으로부터 역할 구조(Role Structure)를 추론할 수 있다. 이를 통해 정책은 개별 기술뿐만 아니라 전체 팀을 효과적으로 만드는 책임 분담 패턴까지 재현할 수 있다.

통신(Communication) 역시 시연된 행동의 일부가 될 수 있다. 전문가 팀의 시연은 로봇들이 언제 위치, 의도(Intent), 작업 상태, 불확실성(Uncertainty), 지원 요청을 공유해야 하는지를 보여줄 수 있다. 학습 시스템은 명시적인 통신 행동을 모방하거나 실제 행동으로부터 잠재적인 협조 신호(Latent Coordination Signal)를 추론할 수 있다. 이를 통해 메시지 교환을 별도로 설계된 메커니즘으로만 취급하지 않고 협력의 기능적인 구성요소로 학습할 수 있다.

시간적 동기화(Temporal Synchronization)는 또 다른 중요한 과제이다. 협력 작업에서는 특정한 순서 또는 제한된 시간 관계 안에서 행동해야 하는 경우가 많다. 하나의 로봇은 다른 로봇이 특정 위치에 도달하거나, 물체를 고정하거나, 통로를 확보하거나, 검사를 완료할 때까지 기다려야 할 수 있다. 따라서 시연에 포함된 시간적 구조(Temporal Structure)는 작업 단계, 이벤트 의존성(Event Dependency), 순환 메모리(Recurrent Memory) 또는 다른 시퀀스 인식 표현(Sequence-Aware Representation)을 통해 보존되어야 한다.

협력 시연(Cooperative Demonstration)은 복구(Recovery)에 관한 가치 있는 사례도 제공할 수 있다. 전문가 운영자는 차단된 경로, 파지 실패, 통신 지연, 위치추정 오류(Localization Error), 예상하지 못한 인간 활동에 대해 수동으로 명시하기 어려운 방식으로 대응하는 경우가 많다. 이러한 에피소드를 기록하면 학습 시스템은 정상적인 협력 행동뿐만 아니라 정상적인 실행이 방해받았을 때 팀이 행동을 재구성하는 방법까지 모방할 수 있다.

공유 경험(Shared Experience)은 플릿이 이용할 수 있는 시연 데이터의 양과 다양성을 증가시킨다. 일부 로봇에서 성공적으로 학습되거나 시연된 행동을 저장하고 평가한 뒤 다른 로봇이 재사용할 수 있다. 서로 다른 환경에서 반복적으로 수집된 시연은 필수적인 협조 패턴과 우연한 세부 요소를 구분하는 데 도움을 준다. 그 결과 데이터셋은 협력 작업, 기술, 복구 방법, 상호작용 전략을 포함하는 플릿 규모 라이브러리(Fleet-Scale Library)로 점진적으로 발전할 수 있다.

이기종 플릿(Heterogeneous Fleet)에서는 서로 다른 체화가 동일한 물리적 행동을 그대로 모방할 수 없기 때문에 신중한 전이가 필요하다. 자율이동로봇(AMR), 4족 보행 로봇(Quadruped), 무인항공기(UAV), 매니퓰레이터(Manipulator), 휴머노이드(Humanoid)는 이동성, 센싱, 동역학(Dynamics), 행동 공간(Action Space)이 서로 다르다. 대신 협력적 모방학습은 탐색(Explore), 관측(Observe), 운송(Transport), 지원(Support), 중계(Relay), 조작(Manipulate)과 같은 작업 수준 개념을 전이하고, 각 체화가 자신의 제어기와 역량을 이용하여 할당된 행동을 구현하도록 할 수 있다.

중앙집중식 학습과 분산 실행(Centralized Training and Distributed Execution, CTDE)은 협력적 모방학습을 지원할 수 있다. 학습 과정에서는 여러 로봇의 동기화된 시연을 활용하여 팀 행동, 역할, 상호작용, 결과에 대한 전역 맥락(Global Context)을 확보할 수 있다. 실행 단계에서는 각 로봇이 로컬에서 이용 가능한 관측과 허용된 통신을 기반으로 분산 정책(Decentralized Policy)을 사용할 수 있다. 따라서 풍부한 시연을 활용하면서도 지속적인 중앙집중식 제어에 의존하지 않을 수 있다.

모방학습과 다중 에이전트 강화학습(Multi-Agent Reinforcement Learning)도 서로 보완적으로 활용할 수 있다. 시연은 유용한 초기 정책(Initial Policy)을 제공하고 실제 로봇에서 요구되는 위험하거나 비효율적인 탐색의 양을 줄일 수 있다. 이후 강화학습은 모방된 정책을 개선하고, 시연에서 다루지 않은 조건에 적응하며, 집단 목표(Collective Objective)를 최적화할 수 있다. 이러한 결합은 전문가 사례를 이용할 수 있지만 모든 운영 상황을 시연으로 포괄할 수 없는 경우에 특히 유용하다.

모방은 유용한 전문성뿐만 아니라 체계적인 약점도 함께 재현할 수 있기 때문에 시연 품질(Demonstration Quality)은 매우 중요하다. 일관성이 없는 운영자, 비효율적인 협조, 안전하지 않은 지름길, 동기화가 제대로 이루어지지 않은 시연은 바람직하지 않은 행동을 유입할 수 있다. 따라서 플릿 학습 파이프라인(Fleet Learning Pipeline)은 시연 출처(Provenance)를 추적하고, 결과를 평가하며, 저품질 에피소드를 필터링하고, 안전 제약을 유지하며, 공유 학습 데이터에 포함하기 전에 신뢰도 또는 품질 지표를 부여해야 한다.

학습된 협조가 로봇 사이 또는 인간과의 물리적 상호작용을 포함하는 경우 안전(Safety)은 특히 중요하다. 전문가 데이터에 등장했다는 이유만으로 모방된 행동이 자동으로 허용되어서는 안 된다. 충돌 제약(Collision Constraint), 안전거리 요구사항, 액추에이터 한계, 제한 구역, 인간 안전 규칙, 런타임 보증(Runtime Assurance)은 학습 정책과 독립적으로 유지될 수 있다. 이를 통해 모방학습으로 행동을 향상시키면서 기존의 안전 메커니즘이 허용할 수 없는 행동을 제한하도록 할 수 있다.

궁극적으로 협력적 모방학습(Cooperative Imitation Learning)은 성공적인 팀 행동을 재사용 가능한 플릿 지식(Fleet Knowledge)으로 변환하는 메커니즘을 제공한다. 시연은 로봇들이 어떻게 협조하고, 전문화하며, 통신하고, 행동을 동기화하고, 실패에서 복구하는지를 포착하며, 학습은 이러한 사례를 전체 플릿에 재배포할 수 있는 정책과 기술(Skill)로 변환한다. 집단 학습(Collective Learning)에서 이는 공유 경험을 정책 공유(Policy Sharing), 로봇 간 전이(Cross-Robot Transfer), 지속학습(Continual Learning), 더욱 발전된 다중 로봇 피지컬 AI(Multi-Robot Physical AI) 시스템과 연결한다.

##  

## 05.06. Federated Robot Learning

![](images/image7.png){width="7.268055555555556in" height="7.268055555555556in"}

![](images/image8.png){width="7.268055555555556in" height="7.268055555555556in"}

Federated Robot Learning extends federated learning to embodied systems by allowing multiple robots to improve a shared model without continuously transferring their raw operational data to a central repository. Each robot learns from locally collected observations and experiences, produces model updates, and contributes those updates to an aggregation process. The resulting global model can then be redistributed across the participating robot fleet.

The central principle is to move learning toward the data rather than moving all data toward a centralized training system. Cameras, LiDARs, tactile sensors, navigation logs, manipulation trajectories, and interaction histories can remain on individual robots or local sites. Instead of uploading complete datasets, robots perform local training and communicate parameters, gradients, adapters, or other compact model updates required for collective improvement.

A typical federated learning round begins when a global model is distributed to selected robots. Each participating robot uses its local dataset to perform one or more training steps and generates an updated local model. These updates are transmitted to an aggregation system, where they are combined into a new global model. The improved model is subsequently redistributed, creating repeated cycles of local learning, aggregation, validation, and deployment.

This architecture is attractive when raw robot data are expensive, sensitive, or impractical to centralize. Physical robots can generate large volumes of high-bandwidth sensor information, while communication networks may provide limited or intermittent connectivity. Federated learning reduces the requirement to transfer complete sensor histories and allows useful learning to occur where the experience was originally generated, although model updates themselves still consume communication resources.

Federated robot learning differs from conventional federated learning because robot data arise from physical interaction rather than passive digital records. A robot\'s dataset depends on its policy, embodiment, environment, assigned tasks, sensor configuration, and previous experiences. Consequently, data collected by different robots are rarely identically distributed, creating substantial statistical heterogeneity across the fleet and making simple model averaging potentially insufficient.

Non-independent and identically distributed data, commonly described as non-IID data, are therefore a central challenge. One warehouse robot may primarily encounter narrow aisles and pallets, while another operates near loading docks and humans. An outdoor robot may experience terrain and weather conditions absent from indoor datasets. Federated aggregation must combine these different experience distributions without allowing dominant or highly repetitive participants to overwhelm less common but valuable knowledge.

Hardware and embodiment heterogeneity introduce additional complexity. Robots may have different processors, sensors, control frequencies, mobility mechanisms, manipulators, and computational budgets. Some robots can perform substantial local training, while others may support only lightweight adaptation. Federated robot learning may therefore require heterogeneous training schedules, selective parameter updates, shared representation layers, adapters, or embodiment-specific model components.

Aggregation determines how distributed learning contributions become collective knowledge. Basic approaches can combine local model parameters according to the amount of training data contributed by each robot. More advanced approaches may consider data quality, novelty, confidence, robot reliability, task relevance, environmental diversity, or model performance. The objective is not merely to average every contribution equally, but to construct a global model that benefits from diverse fleet experience.

Communication efficiency is essential because federated learning can require many rounds of model exchange. Large robot models may contain millions or billions of parameters, making repeated full-model transmission costly. Update compression, quantization, sparsification, selective layer training, parameter-efficient fine-tuning, and less frequent synchronization can reduce communication requirements while preserving much of the benefit of collaborative learning.

Participation does not need to be synchronous. In real fleets, some robots may be operating, charging, disconnected, undergoing maintenance, or executing safety-critical missions when a training round begins. Synchronous federated learning can wait for a selected group of participants, whereas asynchronous approaches can incorporate updates as robots become available. The architecture must tolerate variable availability without allowing delayed or obsolete updates to destabilize the shared model.

Model staleness becomes important when updates are generated from different global model versions. A robot that remains offline for a long period may eventually return an update based on an outdated policy or representation. Version tracking, update timestamps, compatibility checks, recency weighting, and rejection of excessively stale contributions help maintain consistency as the fleet learns under intermittent connectivity and different operating schedules.

Privacy is an important motivation for federated learning, but keeping raw data local does not automatically guarantee privacy. Model updates can potentially reveal information about local training data under certain conditions. Secure aggregation, access control, encryption, update clipping, privacy-preserving techniques, and carefully designed data governance may therefore be required when robots operate in factories, hospitals, homes, public spaces, or other sensitive environments.

Security introduces another challenge because a compromised or malfunctioning robot may submit harmful updates. Model poisoning, corrupted training data, faulty sensors, or unauthorized participants can degrade the global model and potentially affect many robots after redistribution. Federated robot learning therefore benefits from robot authentication, update validation, anomaly detection, robust aggregation, provenance tracking, and controlled deployment of newly aggregated models.

Personalization can coexist with federation. A single global model may capture knowledge useful across the fleet, while each robot maintains local parameters that reflect its hardware, environment, task distribution, or operating history. Shared backbone models combined with local adapters or specialized policy heads provide one way to preserve collective knowledge while allowing individual robots to adapt to conditions that should not be forced into a universal fleet policy.

Federated learning can also operate hierarchically. Robots within one facility may first aggregate updates through an edge or on-premise server, while multiple sites subsequently contribute higher-level updates to a broader fleet model. Such hierarchical federation can reduce long-distance communication, preserve site-specific knowledge, and support large deployments containing many robots distributed across factories, warehouses, campuses, cities, or geographic regions.

Validation remains necessary before an aggregated model is distributed to operational robots. A global update that improves average training performance may degrade a rare task, particular embodiment, or safety-critical scenario. Models can therefore be evaluated against reference datasets, simulation scenarios, replayed fleet episodes, robot-specific benchmarks, and safety tests before staged deployment. Versioning and rollback provide additional protection against unexpected degradation.

Federated robot learning ultimately creates a distributed learning loop in which physical experience remains decentralized while useful knowledge flows across the fleet. Robots collect experience, learn locally, contribute validated updates, receive improved shared models, and continue operating under new conditions. Within collective learning, this approach complements shared experience, CTDE, distributed model updates, policy sharing, cross-robot transfer, and continual learning.

The broader objective is not simply to avoid central data storage, but to enable scalable collective intelligence across robots that cannot or should not pool all of their raw experience. By combining local adaptation with global aggregation, Federated Robot Learning allows distributed Physical AI systems to learn from diverse environments while respecting communication, embodiment, privacy, security, and operational constraints. It therefore provides an important architecture for continuously improving robot fleets at scale.

연합 로봇 학습(Federated Robot Learning)은 여러 로봇이 원시 운영 데이터(Raw Operational Data)를 중앙 저장소(Central Repository)로 지속적으로 전송하지 않고도 공유 모델(Shared Model)을 개선할 수 있도록 연합학습(Federated Learning)을 체화 시스템(Embodied System)으로 확장한 것이다. 각 로봇은 로컬에서 수집된 관측과 경험을 이용하여 학습하고 모델 업데이트(Model Update)를 생성한 뒤 이를 통합 과정(Aggregation Process)에 제공한다. 이후 생성된 전역 모델(Global Model)은 참여하는 로봇 플릿(Robot Fleet)에 다시 배포될 수 있다.

핵심 원리는 모든 데이터를 중앙집중식 학습 시스템으로 이동시키는 대신 학습을 데이터가 존재하는 위치로 이동시키는 것이다. 카메라, 라이다(LiDAR), 촉각 센서(Tactile Sensor), 내비게이션 로그(Navigation Log), 조작 궤적(Manipulation Trajectory), 상호작용 이력은 개별 로봇 또는 로컬 사이트(Local Site)에 유지할 수 있다. 전체 데이터셋을 업로드하는 대신 로봇이 로컬 학습(Local Training)을 수행하고 집단적 개선에 필요한 파라미터, 그래디언트(Gradient), 어댑터(Adapter) 또는 기타 압축된 모델 업데이트를 전달한다.

일반적인 연합학습 라운드(Federated Learning Round)는 전역 모델을 선택된 로봇에 배포하면서 시작한다. 참여 로봇은 자신의 로컬 데이터셋(Local Dataset)을 이용하여 하나 이상의 학습 단계를 수행하고 업데이트된 로컬 모델(Local Model)을 생성한다. 이러한 업데이트는 통합 시스템(Aggregation System)으로 전송되어 새로운 전역 모델로 결합된다. 이후 개선된 모델이 다시 배포되면서 로컬 학습, 통합, 검증(Validation), 배포(Deployment)가 반복되는 순환 구조를 형성한다.

이러한 아키텍처는 원시 로봇 데이터의 중앙집중화가 비용이 많이 들거나 민감하거나 현실적으로 어려운 경우에 유용하다. 물리적 로봇은 대용량의 고대역폭 센서 정보를 생성할 수 있지만 통신 네트워크는 제한적이거나 간헐적인 연결만 제공할 수 있다. 연합학습은 전체 센서 이력을 전송해야 하는 요구를 줄이고 경험이 생성된 위치에서 유용한 학습을 수행할 수 있게 한다. 다만 모델 업데이트 자체에도 여전히 통신 자원이 필요하다.

연합 로봇 학습은 로봇 데이터가 수동적으로 축적되는 디지털 기록이 아니라 물리적 상호작용(Physical Interaction)을 통해 생성된다는 점에서 일반적인 연합학습과 차이가 있다. 로봇의 데이터셋은 정책(Policy), 체화(Embodiment), 환경, 할당된 작업, 센서 구성, 이전 경험에 따라 달라진다. 따라서 서로 다른 로봇이 수집한 데이터는 동일한 분포를 따르는 경우가 드물며, 플릿 전체에 상당한 통계적 이질성(Statistical Heterogeneity)이 발생하여 단순한 모델 평균화만으로는 충분하지 않을 수 있다.

독립적이고 동일한 분포를 따르지 않는 데이터(Non-Independent and Identically Distributed Data), 즉 비독립·비동일분포 데이터(Non-IID Data)는 핵심적인 문제이다. 한 창고 로봇은 주로 좁은 통로와 팔레트를 경험하는 반면 다른 로봇은 하역장과 사람 주변에서 동작할 수 있다. 실외 로봇은 실내 데이터셋에는 존재하지 않는 지형과 날씨를 경험할 수 있다. 연합 통합(Federated Aggregation)은 지배적이거나 반복적인 참여자의 데이터가 드물지만 가치 있는 지식을 압도하지 않도록 서로 다른 경험 분포를 결합해야 한다.

하드웨어와 체화의 이질성(Hardware and Embodiment Heterogeneity)은 추가적인 복잡성을 발생시킨다. 로봇은 서로 다른 프로세서, 센서, 제어 주기(Control Frequency), 이동 메커니즘, 매니퓰레이터(Manipulator), 연산 자원(Computational Budget)을 가질 수 있다. 일부 로봇은 상당한 규모의 로컬 학습을 수행할 수 있지만 다른 로봇은 경량 적응(Lightweight Adaptation)만 가능할 수 있다. 따라서 연합 로봇 학습에는 이기종 학습 일정, 선택적 파라미터 업데이트, 공유 표현 계층(Shared Representation Layer), 어댑터 또는 체화 특화 모델 구성요소가 필요할 수 있다.

통합(Aggregation)은 분산된 학습 기여가 어떻게 집단 지식(Collective Knowledge)으로 변환되는지를 결정한다. 기본적인 접근법에서는 각 로봇이 제공한 학습 데이터의 양에 따라 로컬 모델 파라미터를 결합할 수 있다. 더욱 발전된 방식에서는 데이터 품질, 새로움(Novelty), 신뢰도(Confidence), 로봇 신뢰성, 작업 관련성, 환경 다양성 또는 모델 성능을 고려할 수 있다. 목적은 모든 기여를 동일하게 평균화하는 것이 아니라 다양한 플릿 경험으로부터 이익을 얻는 전역 모델을 구축하는 것이다.

연합학습은 여러 차례의 모델 교환을 요구할 수 있기 때문에 통신 효율성(Communication Efficiency)이 중요하다. 대규모 로봇 모델은 수백만 또는 수십억 개의 파라미터를 포함할 수 있어 전체 모델을 반복적으로 전송하면 높은 비용이 발생한다. 업데이트 압축(Update Compression), 양자화(Quantization), 희소화(Sparsification), 선택적 계층 학습, 파라미터 효율적 미세조정(Parameter-Efficient Fine-Tuning), 낮은 동기화 빈도 등을 활용하여 협력 학습의 장점을 상당 부분 유지하면서 통신 요구량을 줄일 수 있다.

참여가 반드시 동기식(Synchronous)일 필요는 없다. 실제 플릿에서는 학습 라운드가 시작될 때 일부 로봇이 운영 중이거나 충전 중이거나 연결이 끊겨 있거나 유지보수를 받고 있거나 안전 중요 임무(Safety-Critical Mission)를 수행하고 있을 수 있다. 동기식 연합학습은 선택된 참여자 집단을 기다릴 수 있는 반면, 비동기식 접근법(Asynchronous Approach)은 로봇이 사용 가능한 상태가 될 때 업데이트를 통합할 수 있다. 아키텍처는 지연되거나 오래된 업데이트가 공유 모델을 불안정하게 만들지 않으면서 가변적인 가용성을 처리해야 한다.

업데이트가 서로 다른 전역 모델 버전에서 생성되는 경우 모델 노후화(Model Staleness)가 중요해진다. 오랜 기간 오프라인 상태였던 로봇은 결국 오래된 정책이나 표현을 기반으로 생성한 업데이트를 반환할 수 있다. 버전 추적(Version Tracking), 업데이트 타임스탬프(Update Timestamp), 호환성 검사(Compatibility Check), 최신성 가중치(Recency Weighting), 지나치게 오래된 기여의 거부 등을 통해 간헐적인 연결성과 서로 다른 운영 일정 속에서도 플릿 학습의 일관성을 유지할 수 있다.

프라이버시(Privacy)는 연합학습의 중요한 동기이지만 원시 데이터를 로컬에 유지한다고 해서 자동으로 프라이버시가 보장되는 것은 아니다. 특정 조건에서는 모델 업데이트를 통해 로컬 학습 데이터에 관한 정보가 노출될 가능성이 있다. 따라서 로봇이 공장, 병원, 가정, 공공장소 또는 기타 민감한 환경에서 운영되는 경우 보안 통합(Secure Aggregation), 접근 제어(Access Control), 암호화(Encryption), 업데이트 클리핑(Update Clipping), 프라이버시 보호 기법(Privacy-Preserving Technique), 적절한 데이터 거버넌스(Data Governance)가 필요할 수 있다.

손상되거나 오작동하는 로봇이 유해한 업데이트를 제출할 수 있기 때문에 보안(Security)은 또 다른 과제를 제기한다. 모델 포이즈닝(Model Poisoning), 손상된 학습 데이터, 결함 센서 또는 승인되지 않은 참여자는 전역 모델의 성능을 저하시키고 재배포 이후 다수의 로봇에 영향을 미칠 수 있다. 따라서 연합 로봇 학습에는 로봇 인증(Robot Authentication), 업데이트 검증(Update Validation), 이상 탐지(Anomaly Detection), 강건한 통합(Robust Aggregation), 출처 추적(Provenance Tracking), 새롭게 통합된 모델의 통제된 배포가 중요하다.

개인화(Personalization)는 연합학습과 함께 적용할 수 있다. 하나의 전역 모델이 전체 플릿에 유용한 지식을 학습하는 동시에 각 로봇은 자신의 하드웨어, 환경, 작업 분포 또는 운영 이력을 반영하는 로컬 파라미터(Local Parameter)를 유지할 수 있다. 공유 백본 모델(Shared Backbone Model)과 로컬 어댑터(Local Adapter) 또는 특화된 정책 헤드(Specialized Policy Head)를 결합하면 집단 지식을 유지하면서 모든 로봇에 강제로 동일한 플릿 정책을 적용하지 않고 개별 조건에 적응할 수 있다.

연합학습은 계층적으로(Hierarchically) 구성할 수도 있다. 하나의 시설에 속한 로봇들이 먼저 엣지(Edge) 또는 온프레미스 서버(On-Premise Server)를 통해 업데이트를 통합하고, 이후 여러 사이트가 더 광범위한 플릿 모델에 상위 수준의 업데이트를 제공할 수 있다. 이러한 계층적 연합(Hierarchical Federation)은 장거리 통신을 줄이고 사이트 특화 지식을 유지하면서 공장, 창고, 캠퍼스, 도시 또는 여러 지역에 분산된 대규모 로봇 배포를 지원할 수 있다.

통합된 모델을 실제 운영 로봇에 배포하기 전에 검증 과정이 필요하다. 평균 학습 성능이 향상된 전역 업데이트라도 드문 작업, 특정 체화 또는 안전 중요 시나리오의 성능을 저하시킬 수 있다. 따라서 모델은 단계적 배포(Staged Deployment) 전에 참조 데이터셋, 시뮬레이션 시나리오, 재현된 플릿 에피소드(Replayed Fleet Episode), 로봇 특화 벤치마크, 안전 시험을 통해 평가할 수 있다. 버전 관리(Versioning)와 롤백(Rollback)은 예상하지 못한 성능 저하에 대한 추가적인 보호 기능을 제공한다.

궁극적으로 연합 로봇 학습은 물리적 경험은 분산된 상태로 유지하면서 유용한 지식은 플릿 전체로 흐르는 분산 학습 루프(Distributed Learning Loop)를 형성한다. 로봇은 경험을 수집하고 로컬에서 학습하며 검증된 업데이트를 제공하고, 개선된 공유 모델을 전달받아 새로운 조건에서 계속 운영한다. 집단 학습(Collective Learning)에서 이러한 접근법은 공유 경험(Shared Experience), 중앙집중식 학습과 분산 실행(CTDE), 분산 모델 업데이트(Distributed Model Updates), 정책 공유(Policy Sharing), 로봇 간 전이(Cross-Robot Transfer), 지속학습(Continual Learning)을 상호 보완한다.

더 넓은 관점에서의 목표는 단순히 중앙 데이터 저장을 피하는 것이 아니라 모든 원시 경험을 하나의 장소에 통합할 수 없거나 통합해서는 안 되는 로봇들 사이에서 확장 가능한 집단 지능(Scalable Collective Intelligence)을 구현하는 것이다. 연합 로봇 학습은 로컬 적응(Local Adaptation)과 전역 통합(Global Aggregation)을 결합함으로써 통신, 체화, 프라이버시, 보안, 운영상의 제약을 고려하면서 분산된 피지컬 AI(Distributed Physical AI) 시스템이 다양한 환경으로부터 공동으로 학습하도록 한다. 따라서 지속적으로 발전하는 대규모 로봇 플릿을 구현하기 위한 중요한 학습 아키텍처를 제공한다.

##  

## 05.07. Distributed Model Updates

![](images/image9.png){width="7.268055555555556in" height="7.268055555555556in"}

Distributed model updates allow a robot fleet to improve shared intelligence without requiring every learning event to pass through a single centralized training process. Individual robots, edge nodes, or local sites can generate model changes from their own operational experience and propagate useful updates across the network. Collective learning therefore becomes an ongoing exchange of learned information rather than a sequence of isolated retraining events.

The information exchanged between robots does not always need to be a complete model. A distributed update may contain changed parameters, gradients, adapter weights, policy components, embeddings, statistics, or selected knowledge modules. By transmitting only what has changed, the system can reduce communication and storage requirements while allowing robots to benefit from learning performed elsewhere in the fleet.

A basic update cycle begins when a robot collects new experience and performs local adaptation. The resulting model change is evaluated locally and packaged together with metadata describing its source, model version, task, environment, time, and confidence. The update can then be transmitted to neighboring robots, an edge server, an on-premise learning system, or another aggregation node depending on the architecture of the fleet.

Distributed updates differ from simple software distribution because learned parameters depend on data distributions and operational context. An update that improves navigation in one warehouse may not improve performance in an outdoor environment or on a robot with different sensors. The system must therefore understand where an update originated and determine whether its learned information is relevant to the receiving robot before applying it.

Model version management becomes essential when many robots learn simultaneously. Different robots may begin from different model versions and produce updates at different times. Without explicit version information, incompatible parameters may be combined or an older update may overwrite more recent knowledge. Version identifiers, update lineage, timestamps, compatibility rules, and dependency tracking help preserve consistency across a continuously evolving fleet.

Synchronous updating provides one method for maintaining consistency. A group of robots can train from a common model version, submit their updates within a defined learning round, and wait while those contributions are aggregated. This simplifies coordination and produces a clear sequence of global model versions, but slow or disconnected robots can delay progress when the system requires all selected participants to complete their local training.

Asynchronous updates provide greater flexibility for operational robot fleets. Robots can contribute learning results whenever they have sufficient data, computational availability, or network connectivity. The shared model can therefore evolve without waiting for every participant. However, asynchronous operation introduces model staleness because an update may have been generated from a model that has already been replaced by several newer versions.

Staleness can be controlled by comparing the base version of an incoming update with the current model. Recent updates may receive greater weight, while significantly outdated contributions can be transformed, re-evaluated, or rejected. Temporal weighting and compatibility checks prevent old information from dominating current learning while still allowing useful rare experiences from intermittently connected robots to contribute to collective knowledge.

Communication topology also influences how updates propagate. A centralized topology sends local changes to one aggregation server, whereas hierarchical architectures first combine updates at edge or site-level nodes. Peer-to-peer systems may allow robots to exchange updates directly with nearby teammates. Hybrid architectures can combine local peer sharing, on-premise aggregation, and higher-level fleet synchronization according to communication availability and operational scale.

Peer-to-peer model exchange can be valuable when robots operate beyond reliable infrastructure. Nearby robots may exchange selected skills, representations, or policy updates through local communication without contacting a remote server. This can accelerate adaptation in field operations, but it also requires mechanisms for determining trust, compatibility, and update quality because information can spread through the fleet without centralized inspection.

Bandwidth limitations encourage parameter-efficient update strategies. Instead of transmitting an entire foundation model, robots can exchange low-rank adapters, selected layers, sparse parameter differences, quantized updates, or task-specific heads. These approaches reduce network traffic and can preserve a stable shared backbone while allowing selected capabilities to evolve more rapidly across robots and operational environments.

Update selection is equally important because not every local change deserves fleet-wide propagation. A model modification based on repetitive or low-confidence experience may offer little value, while an update derived from a rare failure or successful recovery may be highly useful. Novelty, performance improvement, uncertainty reduction, task relevance, data quality, and safety evaluation can be used to determine which updates should be shared.

Conflicting updates can occur when robots learn different responses to similar situations. One robot may adapt to a slippery floor while another learns from high-friction terrain, producing parameter changes that interfere when combined. Aggregation mechanisms must therefore identify compatible, complementary, or contradictory learning signals. Clustering, weighting, specialization, or separate model branches can preserve useful diversity instead of forcing all knowledge into one universal model.

Security and trust become critical because model updates directly influence future robot behavior. A malfunctioning, compromised, or poorly calibrated robot could distribute harmful parameters that degrade many agents. Authentication, provenance tracking, anomaly detection, update validation, secure communication, and robust aggregation help prevent corrupted or malicious learning signals from propagating throughout the collective system.

Validation should occur at multiple stages of the update pipeline. A robot may first test its local adaptation against stored examples or safety constraints before sharing it. Aggregation nodes can evaluate combined updates in simulation, replay buffers, benchmarks, or digital twins. Candidate models can then be deployed gradually to selected robots before wider release, with monitoring and rollback mechanisms protecting operational stability.

Distributed model updates also support personalization. Robots can share a common backbone while maintaining local adapters, calibration components, policy heads, or environment-specific parameters. Fleet updates improve generally useful representations, whereas local components preserve specialization. This architecture is particularly valuable for heterogeneous robots because collective learning does not require every embodiment to converge toward exactly the same model.

The broader result is a continuous distributed learning network in which experience can generate improvements at many points in the fleet. Robots collect data, adapt locally, evaluate changes, exchange useful updates, integrate knowledge from other agents, and continue operating with improved models. Distributed model updates therefore connect federated learning, policy sharing, cross-robot transfer, continual learning, and fleet-wide adaptation into a scalable mechanism for collective Physical AI.

분산 모델 업데이트(Distributed Model Updates)는 모든 학습 이벤트가 하나의 중앙집중식 학습 과정(Centralized Training Process)을 거치지 않고도 로봇 플릿(Robot Fleet)이 공유 지능(Shared Intelligence)을 향상시킬 수 있도록 한다. 개별 로봇, 엣지 노드(Edge Node), 로컬 사이트(Local Site)는 자체 운영 경험으로부터 모델 변경 사항을 생성하고 유용한 업데이트를 네트워크 전체로 전파할 수 있다. 따라서 집단 학습(Collective Learning)은 고립된 재학습 이벤트의 연속이 아니라 학습된 정보를 지속적으로 교환하는 과정으로 발전한다.

로봇 사이에서 교환되는 정보가 항상 완전한 모델(Complete Model)일 필요는 없다. 분산 업데이트(Distributed Update)는 변경된 파라미터, 그래디언트(Gradient), 어댑터 가중치(Adapter Weight), 정책 구성요소(Policy Component), 임베딩(Embedding), 통계 정보 또는 선택된 지식 모듈(Knowledge Module)을 포함할 수 있다. 변경된 부분만 전송함으로써 시스템은 통신 및 저장 요구량을 줄이면서 플릿의 다른 위치에서 수행된 학습의 이점을 여러 로봇이 공유하도록 할 수 있다.

기본적인 업데이트 주기(Update Cycle)는 로봇이 새로운 경험을 수집하고 로컬 적응(Local Adaptation)을 수행하면서 시작된다. 생성된 모델 변경 사항은 로컬에서 평가되고 출처, 모델 버전(Model Version), 작업, 환경, 시간, 신뢰도(Confidence)를 설명하는 메타데이터(Metadata)와 함께 패키지화된다. 이후 플릿 아키텍처에 따라 업데이트를 인접 로봇, 엣지 서버(Edge Server), 온프레미스 학습 시스템(On-Premise Learning System), 또는 다른 통합 노드(Aggregation Node)로 전송할 수 있다.

분산 업데이트는 학습된 파라미터가 데이터 분포(Data Distribution)와 운영 맥락(Operational Context)에 따라 달라진다는 점에서 단순한 소프트웨어 배포와 다르다. 한 창고에서 내비게이션 성능을 향상시킨 업데이트가 실외 환경이나 다른 센서를 사용하는 로봇에서는 동일한 성능 향상을 제공하지 않을 수 있다. 따라서 시스템은 업데이트가 어디에서 생성되었는지를 파악하고 학습된 정보가 업데이트를 수신하는 로봇과 관련성이 있는지를 적용 전에 판단해야 한다.

여러 로봇이 동시에 학습하는 경우 모델 버전 관리(Model Version Management)가 필수적이다. 서로 다른 로봇은 서로 다른 모델 버전에서 시작하여 서로 다른 시점에 업데이트를 생성할 수 있다. 명확한 버전 정보가 없다면 호환되지 않는 파라미터가 결합되거나 오래된 업데이트가 더 최신의 지식을 덮어쓸 수 있다. 버전 식별자(Version Identifier), 업데이트 계보(Update Lineage), 타임스탬프(Timestamp), 호환성 규칙(Compatibility Rule), 의존성 추적(Dependency Tracking)은 지속적으로 발전하는 플릿 전체의 일관성을 유지하는 데 도움을 준다.

동기식 업데이트(Synchronous Updating)는 일관성을 유지하기 위한 하나의 방법을 제공한다. 여러 로봇이 공통 모델 버전에서 학습을 시작하고 정의된 학습 라운드(Learning Round) 내에서 업데이트를 제출한 뒤 해당 기여가 통합될 때까지 기다릴 수 있다. 이러한 방식은 협조를 단순화하고 명확한 전역 모델 버전의 흐름을 만들지만, 선택된 모든 참여자의 로컬 학습 완료가 요구되는 경우 느리거나 연결이 끊어진 로봇이 전체 학습 진행을 지연시킬 수 있다.

비동기식 업데이트(Asynchronous Updates)는 실제 운영 로봇 플릿에 더 높은 유연성을 제공한다. 로봇은 충분한 데이터, 연산 자원 또는 네트워크 연결성을 확보했을 때 언제든지 학습 결과를 제공할 수 있다. 따라서 모든 참여자를 기다리지 않고 공유 모델을 지속적으로 발전시킬 수 있다. 그러나 비동기식 운영에서는 이미 여러 개의 새로운 모델로 교체된 이전 모델을 기반으로 업데이트가 생성될 수 있기 때문에 모델 노후화(Model Staleness) 문제가 발생한다.

노후화(Staleness)는 들어오는 업데이트의 기반 버전(Base Version)과 현재 모델을 비교하여 제어할 수 있다. 최신 업데이트에는 더 높은 가중치를 부여하고, 지나치게 오래된 기여는 변환하거나 재평가하거나 거부할 수 있다. 시간 가중치(Temporal Weighting)와 호환성 검사(Compatibility Check)는 오래된 정보가 현재 학습을 지배하는 것을 방지하면서도 간헐적으로 연결되는 로봇이 경험한 희귀하고 가치 있는 정보가 집단 지식(Collective Knowledge)에 기여하도록 한다.

통신 토폴로지(Communication Topology)는 업데이트가 어떻게 전파되는지에도 영향을 준다. 중앙집중식 토폴로지는 로컬 변경 사항을 하나의 통합 서버(Aggregation Server)로 전송하며, 계층적 아키텍처(Hierarchical Architecture)는 먼저 엣지 또는 사이트 수준 노드에서 업데이트를 결합한다. 피어투피어 시스템(Peer-to-Peer System)은 인접한 로봇끼리 직접 업데이트를 교환하도록 할 수 있다. 하이브리드 아키텍처(Hybrid Architecture)는 통신 가용성과 운영 규모에 따라 로컬 피어 공유, 온프레미스 통합, 상위 수준 플릿 동기화를 결합할 수 있다.

피어투피어 모델 교환(Peer-to-Peer Model Exchange)은 로봇이 안정적인 인프라의 범위를 벗어나 운영될 때 유용할 수 있다. 인접한 로봇들은 원격 서버에 접속하지 않고도 로컬 통신을 통해 선택된 기술(Skill), 표현(Representation), 정책 업데이트(Policy Update)를 교환할 수 있다. 이는 현장 운영에서 적응 속도를 높일 수 있지만, 중앙 검사를 거치지 않고 정보가 플릿으로 확산될 수 있으므로 신뢰성, 호환성, 업데이트 품질을 판단하는 메커니즘이 필요하다.

대역폭 제한(Bandwidth Limitation)은 파라미터 효율적 업데이트 전략(Parameter-Efficient Update Strategy)의 필요성을 높인다. 전체 파운데이션 모델(Foundation Model)을 전송하는 대신 로봇은 저랭크 어댑터(Low-Rank Adapter), 선택된 계층(Selected Layer), 희소 파라미터 차이(Sparse Parameter Difference), 양자화된 업데이트(Quantized Update), 작업 특화 헤드(Task-Specific Head)를 교환할 수 있다. 이러한 접근법은 안정적인 공유 백본(Shared Backbone)을 유지하면서 네트워크 트래픽을 줄이고 선택된 역량이 로봇과 운영 환경 전반에서 더욱 빠르게 발전하도록 할 수 있다.

모든 로컬 변경 사항이 플릿 전체에 전파될 가치가 있는 것은 아니기 때문에 업데이트 선택(Update Selection) 역시 중요하다. 반복적이거나 신뢰도가 낮은 경험을 기반으로 한 모델 변경은 가치가 제한적일 수 있지만, 드문 실패 또는 성공적인 복구에서 생성된 업데이트는 매우 유용할 수 있다. 새로움(Novelty), 성능 향상, 불확실성 감소(Uncertainty Reduction), 작업 관련성(Task Relevance), 데이터 품질, 안전 평가 등을 이용하여 어떤 업데이트를 공유할 것인지 결정할 수 있다.

로봇들이 유사한 상황에 대해 서로 다른 대응을 학습하면 충돌하는 업데이트(Conflicting Updates)가 발생할 수 있다. 하나의 로봇은 미끄러운 바닥에 적응하고 다른 로봇은 마찰력이 높은 지형에서 학습하여 두 파라미터 변경 사항을 결합했을 때 서로 간섭할 수 있다. 따라서 통합 메커니즘은 호환 가능하거나 상호보완적이거나 서로 모순되는 학습 신호를 식별해야 한다. 클러스터링(Clustering), 가중치 적용(Weighting), 전문화(Specialization), 별도의 모델 분기(Model Branch)를 활용하면 모든 지식을 하나의 범용 모델에 강제로 통합하지 않고 유용한 다양성을 유지할 수 있다.

모델 업데이트가 향후 로봇 행동에 직접적인 영향을 미치기 때문에 보안(Security)과 신뢰(Trust)는 매우 중요하다. 오작동하거나 침해되었거나 제대로 캘리브레이션되지 않은 로봇이 유해한 파라미터를 배포하면 다수의 에이전트 성능이 저하될 수 있다. 인증(Authentication), 출처 추적(Provenance Tracking), 이상 탐지(Anomaly Detection), 업데이트 검증(Update Validation), 보안 통신(Secure Communication), 강건한 통합(Robust Aggregation)은 손상되거나 악의적인 학습 신호가 집단 시스템 전체로 확산되는 것을 방지하는 데 도움을 준다.

검증(Validation)은 업데이트 파이프라인(Update Pipeline)의 여러 단계에서 수행되어야 한다. 로봇은 로컬 적응 결과를 공유하기 전에 저장된 사례 또는 안전 제약(Safety Constraint)을 기준으로 먼저 시험할 수 있다. 통합 노드는 결합된 업데이트를 시뮬레이션(Simulation), 리플레이 버퍼(Replay Buffer), 벤치마크(Benchmark), 디지털 트윈(Digital Twin)에서 평가할 수 있다. 이후 후보 모델(Candidate Model)을 일부 로봇에 단계적으로 배포하고 모니터링과 롤백(Rollback) 메커니즘을 통해 운영 안정성을 보호할 수 있다.

분산 모델 업데이트는 개인화(Personalization)도 지원한다. 로봇들은 공통 백본(Common Backbone)을 공유하면서 로컬 어댑터(Local Adapter), 캘리브레이션 구성요소, 정책 헤드(Policy Head), 환경 특화 파라미터(Environment-Specific Parameter)를 개별적으로 유지할 수 있다. 플릿 업데이트는 일반적으로 유용한 표현을 향상시키고 로컬 구성요소는 전문화를 유지한다. 이러한 아키텍처는 집단 학습이 모든 체화를 정확히 동일한 모델로 수렴시킬 필요가 없기 때문에 이기종 로봇(Heterogeneous Robots)에 특히 유용하다.

전체적인 결과는 플릿의 여러 위치에서 경험이 지능 향상으로 연결되는 지속적인 분산 학습 네트워크(Continuous Distributed Learning Network)이다. 로봇은 데이터를 수집하고, 로컬에서 적응하고, 변경 사항을 평가하며, 유용한 업데이트를 교환하고, 다른 에이전트의 지식을 통합한 뒤 개선된 모델로 계속 운영한다. 따라서 분산 모델 업데이트는 연합학습(Federated Learning), 정책 공유(Policy Sharing), 로봇 간 전이(Cross-Robot Transfer), 지속학습(Continual Learning), 플릿 전체 적응(Fleet-Wide Adaptation)을 집단 피지컬 AI(Collective Physical AI)를 위한 확장 가능한 학습 메커니즘으로 연결한다.

##  

## 05.08. Policy and Skill Sharing

![](images/image10.png){width="7.268055555555556in" height="7.268055555555556in"}

Policy and skill sharing allows a multi-robot system to distribute learned behavior directly across the fleet rather than requiring every robot to rediscover useful strategies through independent experience. A policy determines how observations or states are transformed into actions, while a skill represents a reusable behavioral capability that can be invoked within different tasks. Sharing both enables collective experience to become executable knowledge.

Policy sharing is most straightforward when robots have similar embodiments, sensors, action spaces, and operational objectives. A navigation policy learned by one autonomous mobile robot may be transferred to another compatible platform, allowing the receiving robot to benefit immediately from previous training. This reduces duplicated learning effort and allows improvements discovered by one part of the fleet to propagate rapidly to other robots.

A complete policy does not always need to be transferred. Large robot models may contain general perception, reasoning, world modeling, and control components that should remain stable while only selected capabilities change. Robots can therefore exchange policy heads, adapters, selected neural network layers, parameter differences, or task-specific modules. This modular approach reduces communication cost and limits unnecessary modification of already validated capabilities.

Skill sharing operates at a higher behavioral level. A skill may represent docking, obstacle avoidance, object pickup, door traversal, inspection, formation keeping, recovery, or cooperative transport. Instead of transferring every low-level action from a previous trajectory, the fleet can represent the capability through a reusable skill module with defined inputs, outputs, preconditions, termination conditions, and expected outcomes.

This abstraction allows skills to become building blocks for more complex robot behavior. A mission such as warehouse inspection may combine navigation, localization recovery, elevator interaction, visual inspection, anomaly reporting, and charging skills. Once individual capabilities have been learned and validated, planners or higher-level policies can compose them into new task sequences without retraining the complete robot behavior from the beginning.

Skill libraries provide an organizational mechanism for collective learning. Successfully learned capabilities can be registered in a shared repository together with metadata describing the source robot, compatible embodiments, required sensors, environment assumptions, performance, safety constraints, and version. Other robots can search the library for relevant capabilities and determine whether a skill can be executed directly, adapted locally, or rejected as incompatible.

Heterogeneous robot fleets make compatibility particularly important. A navigation policy designed for a wheeled AMR cannot be copied directly to a quadruped or UAV because their dynamics and action spaces differ. However, the higher-level skill objective, such as reaching a target, exploring an area, following another agent, or inspecting an object, may still be transferable. Each embodiment can map the shared skill representation to its own low-level controller.

Policy and skill sharing therefore benefit from separating task knowledge from embodiment-specific execution. Shared representations can describe goals, semantic actions, task phases, constraints, object relationships, or expected outcomes, while local controllers translate these concepts into platform-specific commands. This separation increases transferability and allows collective intelligence to span robots with different mechanical structures and sensing configurations.

Context must accompany shared behavior because a policy that performs well in one environment may be inappropriate elsewhere. Floor friction, lighting, terrain, payload, obstacle density, communication quality, sensor configuration, and human activity can influence performance. Policies and skills should therefore include applicability information that helps receiving robots estimate whether the transferred knowledge matches their current operating conditions.

Performance evidence is also necessary when deciding what should be shared. A skill may have been successful in hundreds of executions, while another may have been generated from only a few experiments. Success rate, uncertainty, task completion time, energy consumption, intervention frequency, safety events, and environmental diversity can provide indicators of maturity. Fleet systems can prioritize well-supported skills while treating experimental capabilities cautiously.

Policy sharing can occur through centralized, hierarchical, or peer-to-peer architectures. A fleet server may maintain validated policies and distribute them to compatible robots, while site-level servers can manage local variants. Robots operating without reliable infrastructure may exchange selected capabilities directly with nearby teammates. The communication topology can therefore adapt to deployment scale, connectivity, and operational requirements.

Peer-to-peer skill sharing is particularly useful when one robot discovers a successful response to a local problem that nearby robots are likely to encounter. A robot that learns how to traverse difficult terrain, recover from a localization failure, or negotiate a temporary obstacle can distribute the relevant capability locally. Rapid sharing converts individual adaptation into immediate team-level benefit without waiting for complete fleet retraining.

Shared skills can also support cooperative behavior. Robots may exchange policies for formation control, cooperative transport, area coverage, task handoff, communication relay, or coordinated exploration. In these cases, the skill is not defined solely by one robot\'s behavior but by relationships among several agents. Shared representations must capture roles, timing, interaction requirements, and communication assumptions needed for coordinated execution.

Safety validation remains essential because learned behavior directly controls physical systems. A policy that improves average task performance may still introduce unsafe behavior in rare situations. Before fleet-wide distribution, candidate skills can be evaluated in simulation, digital twins, replayed failure scenarios, controlled physical tests, and safety-critical benchmarks. Runtime constraints can continue to supervise execution after deployment.

Versioning and rollback are equally important because policies and skills evolve continuously. Each capability should have a traceable version, dependency information, training history, compatibility requirements, and validation status. If a newly distributed skill produces unexpected degradation, robots should be able to return to a previously verified version while the problematic update is isolated and investigated.

Policy and skill sharing also creates the foundation for continual capability accumulation. A fleet does not need to replace all existing knowledge whenever a new behavior is learned. Instead, validated capabilities can be added, refined, specialized, recombined, and transferred over time. The robot fleet gradually develops a growing repertoire of reusable behaviors derived from experiences accumulated across different robots, environments, and missions.

The resulting collective learning process transforms successful behavior into a shared operational asset. Robots generate experience, learn or refine policies, extract reusable skills, validate their performance, publish compatible capabilities, and adapt received knowledge to local conditions. Policy and skill sharing therefore connects distributed model updates, cross-robot experience, transfer learning, continual learning, and coordinated execution into an expanding library of fleet intelligence.

정책 및 기술 공유(Policy and Skill Sharing)는 모든 로봇이 독립적인 경험을 통해 유용한 전략을 다시 학습하도록 하는 대신, 학습된 행동을 로봇 플릿(Robot Fleet) 전체에 직접 배포할 수 있도록 한다. 정책(Policy)은 관측 또는 상태를 행동으로 변환하는 방법을 결정하며, 기술(Skill)은 다양한 작업에서 호출하여 사용할 수 있는 재사용 가능한 행동 역량을 의미한다. 두 가지를 공유하면 집단 경험(Collective Experience)을 실제로 실행 가능한 지식(Executable Knowledge)으로 전환할 수 있다.

정책 공유(Policy Sharing)는 로봇들이 유사한 체화(Embodiment), 센서, 행동 공간(Action Space), 운영 목표를 가지고 있을 때 가장 직접적으로 적용할 수 있다. 하나의 자율이동로봇(Autonomous Mobile Robot, AMR)이 학습한 내비게이션 정책(Navigation Policy)을 호환되는 다른 플랫폼으로 전이하면 수신 로봇은 기존 학습 결과를 즉시 활용할 수 있다. 이를 통해 중복되는 학습 노력을 줄이고 플릿 일부에서 발견된 성능 향상을 다른 로봇으로 빠르게 확산할 수 있다.

항상 완전한 정책(Complete Policy) 전체를 전송할 필요는 없다. 대규모 로봇 모델은 일반적인 인식(Perception), 추론(Reasoning), 월드 모델링(World Modeling), 제어(Control) 구성요소를 포함할 수 있으며, 이러한 부분은 안정적으로 유지하면서 특정 역량만 변경해야 할 수 있다. 따라서 로봇은 정책 헤드(Policy Head), 어댑터(Adapter), 선택된 신경망 계층, 파라미터 차이(Parameter Difference), 작업 특화 모듈(Task-Specific Module)을 교환할 수 있다. 이러한 모듈형 접근법(Modular Approach)은 통신 비용을 줄이고 이미 검증된 역량의 불필요한 변경을 제한한다.

기술 공유(Skill Sharing)는 더 높은 행동 수준에서 이루어진다. 하나의 기술은 도킹(Docking), 장애물 회피(Obstacle Avoidance), 객체 픽업(Object Pickup), 문 통과(Door Traversal), 검사(Inspection), 대형 유지(Formation Keeping), 복구(Recovery), 협력 운송(Cooperative Transport) 등을 나타낼 수 있다. 이전 궤적의 모든 저수준 행동을 전송하는 대신, 플릿은 정의된 입력, 출력, 사전조건(Precondition), 종료 조건(Termination Condition), 예상 결과를 갖는 재사용 가능한 기술 모듈(Skill Module)로 해당 역량을 표현할 수 있다.

이러한 추상화를 통해 기술은 더욱 복잡한 로봇 행동을 구성하기 위한 빌딩 블록(Building Block)이 될 수 있다. 예를 들어 창고 검사 임무는 내비게이션, 위치추정 복구(Localization Recovery), 엘리베이터 상호작용, 시각 검사(Visual Inspection), 이상 보고(Anomaly Reporting), 충전 기술을 결합할 수 있다. 개별 역량을 학습하고 검증한 이후에는 플래너(Planner) 또는 상위 수준 정책이 전체 로봇 행동을 처음부터 다시 학습하지 않고도 이러한 기술을 새로운 작업 순서로 조합할 수 있다.

기술 라이브러리(Skill Library)는 집단 학습(Collective Learning)을 체계적으로 구성하기 위한 메커니즘을 제공한다. 성공적으로 학습된 역량은 출처 로봇, 호환 가능한 체화, 필요한 센서, 환경 가정(Environment Assumption), 성능, 안전 제약(Safety Constraint), 버전을 설명하는 메타데이터(Metadata)와 함께 공유 저장소에 등록할 수 있다. 다른 로봇은 라이브러리에서 필요한 역량을 검색하고 해당 기술을 직접 실행할지, 로컬에서 적응할지, 호환되지 않는 기술로 판단하여 거부할지를 결정할 수 있다.

이기종 로봇 플릿(Heterogeneous Robot Fleet)에서는 호환성(Compatibility)이 특히 중요하다. 바퀴형 자율이동로봇을 위해 설계된 내비게이션 정책을 4족 보행 로봇(Quadruped)이나 무인항공기(UAV)에 직접 복사할 수는 없다. 이들의 동역학(Dynamics)과 행동 공간이 서로 다르기 때문이다. 그러나 목표 지점 도달, 영역 탐색, 다른 에이전트 추종, 객체 검사와 같은 상위 수준의 기술 목표(Skill Objective)는 전이할 수 있으며, 각 체화는 공유 기술 표현을 자체 저수준 제어기(Low-Level Controller)에 연결할 수 있다.

따라서 정책 및 기술 공유는 작업 지식(Task Knowledge)과 체화 특화 실행(Embodiment-Specific Execution)을 분리할 때 더욱 효과적이다. 공유 표현(Shared Representation)은 목표, 의미론적 행동(Semantic Action), 작업 단계(Task Phase), 제약, 객체 관계(Object Relationship), 예상 결과 등을 설명하고, 로컬 제어기는 이러한 개념을 플랫폼 특화 명령(Platform-Specific Command)으로 변환할 수 있다. 이러한 분리는 전이 가능성(Transferability)을 높이고 서로 다른 기계 구조와 센서 구성을 가진 로봇 사이에서도 집단 지능을 공유할 수 있도록 한다.

특정 환경에서 우수한 성능을 보인 정책이 다른 환경에서는 적절하지 않을 수 있으므로 공유 행동에는 맥락(Context)이 함께 제공되어야 한다. 바닥 마찰, 조명, 지형, 적재물(Payload), 장애물 밀도, 통신 품질, 센서 구성, 인간 활동은 정책 성능에 영향을 줄 수 있다. 따라서 정책과 기술에는 수신 로봇이 전이된 지식과 현재 운영 조건의 적합성을 평가할 수 있도록 적용 가능성 정보(Applicability Information)를 포함해야 한다.

무엇을 공유해야 하는지 결정하려면 성능 증거(Performance Evidence)도 필요하다. 어떤 기술은 수백 번의 실행을 통해 성공이 검증되었지만 다른 기술은 소수의 실험만으로 생성되었을 수 있다. 성공률, 불확실성(Uncertainty), 작업 완료 시간, 에너지 소비, 개입 빈도(Intervention Frequency), 안전 이벤트, 환경 다양성은 기술의 성숙도(Maturity)를 판단하는 지표가 될 수 있다. 플릿 시스템은 충분히 검증된 기술을 우선적으로 활용하면서 실험적인 역량은 신중하게 취급할 수 있다.

정책 공유는 중앙집중식(Centralized), 계층적(Hierarchical), 피어투피어(Peer-to-Peer) 아키텍처를 통해 수행할 수 있다. 플릿 서버(Fleet Server)가 검증된 정책을 관리하고 호환되는 로봇에 배포할 수 있으며, 사이트 수준 서버(Site-Level Server)는 로컬 변형(Local Variant)을 관리할 수 있다. 안정적인 인프라 없이 운영되는 로봇은 선택된 역량을 주변 팀원과 직접 교환할 수 있다. 따라서 통신 토폴로지(Communication Topology)는 배포 규모, 연결성, 운영 요구사항에 맞추어 조정할 수 있다.

피어투피어 기술 공유(Peer-to-Peer Skill Sharing)는 하나의 로봇이 주변의 다른 로봇들도 곧 경험할 가능성이 높은 로컬 문제에 대한 성공적인 대응 방법을 발견했을 때 특히 유용하다. 어려운 지형 통과, 위치추정 실패 복구, 임시 장애물 처리 방법을 학습한 로봇은 관련 역량을 주변 로봇에 직접 배포할 수 있다. 이러한 빠른 공유는 전체 플릿의 완전한 재학습을 기다리지 않고 개별 적응(Individual Adaptation)을 즉각적인 팀 수준의 이점으로 전환한다.

공유 기술은 협력 행동(Cooperative Behavior)도 지원할 수 있다. 로봇들은 대형 제어(Formation Control), 협력 운송, 영역 커버리지(Area Coverage), 작업 인계(Task Handoff), 통신 중계(Communication Relay), 협력 탐색(Coordinated Exploration)을 위한 정책을 교환할 수 있다. 이러한 경우 기술은 하나의 로봇 행동만으로 정의되는 것이 아니라 여러 에이전트 사이의 관계를 통해 정의된다. 따라서 공유 표현에는 협력 실행에 필요한 역할, 타이밍, 상호작용 요구사항, 통신 조건이 포함되어야 한다.

학습된 행동이 실제 물리 시스템을 직접 제어하기 때문에 안전 검증(Safety Validation)은 필수적이다. 평균적인 작업 성능을 향상시키는 정책이라도 드문 상황에서는 위험한 행동을 유발할 수 있다. 플릿 전체에 배포하기 전에 후보 기술(Candidate Skill)을 시뮬레이션(Simulation), 디지털 트윈(Digital Twin), 재현된 실패 시나리오, 통제된 물리 시험, 안전 중요 벤치마크(Safety-Critical Benchmark)에서 평가할 수 있다. 배포 이후에도 런타임 제약(Runtime Constraint)을 통해 실행을 지속적으로 감독할 수 있다.

정책과 기술은 지속적으로 발전하기 때문에 버전 관리(Versioning)와 롤백(Rollback) 역시 중요하다. 각각의 역량에는 추적 가능한 버전, 의존성 정보(Dependency Information), 학습 이력, 호환성 요구사항, 검증 상태(Validation Status)가 포함되어야 한다. 새롭게 배포된 기술이 예상하지 못한 성능 저하를 발생시키면 문제가 있는 업데이트를 격리하고 조사하는 동안 로봇이 이전에 검증된 버전으로 복귀할 수 있어야 한다.

정책 및 기술 공유는 지속적인 역량 축적(Continual Capability Accumulation)을 위한 기반도 형성한다. 새로운 행동을 학습할 때마다 플릿이 기존의 모든 지식을 교체할 필요는 없다. 대신 검증된 역량을 시간에 따라 추가하고, 개선하고, 전문화하고, 재조합하며, 다른 로봇으로 전이할 수 있다. 이를 통해 로봇 플릿은 서로 다른 로봇, 환경, 임무에서 축적된 경험으로부터 재사용 가능한 행동 레퍼토리(Behavior Repertoire)를 지속적으로 확장할 수 있다.

결과적으로 집단 학습 과정은 성공적인 행동을 공유 가능한 운영 자산(Shared Operational Asset)으로 변환한다. 로봇은 경험을 생성하고, 정책을 학습하거나 개선하며, 재사용 가능한 기술을 추출하고, 성능을 검증하고, 호환 가능한 역량을 공유하며, 전달받은 지식을 로컬 조건에 적응시킨다. 따라서 정책 및 기술 공유는 분산 모델 업데이트(Distributed Model Updates), 로봇 간 경험(Cross-Robot Experience), 전이학습(Transfer Learning), 지속학습(Continual Learning), 협조 실행(Coordinated Execution)을 지속적으로 확장되는 플릿 지능(Fleet Intelligence) 라이브러리로 연결한다.

##  

## 05.09. Experience Replay Across Robots

![](images/image11.png){width="7.268055555555556in" height="7.268055555555556in"}

Experience replay across robots extends the idea of replay memory from individual reinforcement learning to a shared fleet-level learning process. Instead of each robot learning only from trajectories generated by its own operation, experiences collected by many robots can be stored, selected, and reused during later training. This allows physical interactions generated once by one robot to contribute repeatedly to learning across the wider multi-robot system.

A robot experience can contain observations, states, actions, rewards, next states, task outcomes, communication events, failures, interventions, and contextual metadata. When experiences from multiple robots are combined, the replay system becomes more than a simple memory buffer. It forms a distributed record of how different agents behaved under different environmental conditions, embodiments, policies, tasks, and operational constraints.

The primary advantage of cross-robot replay is improved data efficiency. Physical robot experience is expensive because collecting it consumes time, energy, hardware life, human supervision, and operational resources. Reusing previously collected trajectories allows learning algorithms to extract additional value from existing interactions. One robot\'s difficult experience can therefore improve policies used by robots that have never directly encountered the same situation.

Experience diversity is another major benefit. Individual robots usually operate within limited regions of the overall environment distribution. One robot may encounter crowded corridors, another slippery terrain, another unusual objects, and another communication failures. Combining these experiences expands the learning distribution and helps models develop behaviors that generalize beyond the narrow operating history of any single robot.

Replay becomes especially valuable for rare events. Successful routine operations can dominate fleet datasets, while collisions, localization failures, unusual obstacles, failed grasps, communication loss, emergency stops, and recovery behaviors may occur infrequently. If these rare episodes are preserved and replayed with appropriate priority, the fleet can continue learning from them long after the original event occurred.

A shared replay buffer can be organized centrally, hierarchically, or in distributed form. A centralized repository may collect selected trajectories from the entire fleet, while site-level buffers can preserve experiences relevant to particular facilities. Individual robots may also maintain local buffers and exchange selected episodes with nearby agents. Hybrid architectures can combine these levels according to bandwidth, storage capacity, privacy, and operational requirements.

Not every experience should be replayed with equal probability. Uniform sampling is simple but can repeatedly select common, low-information trajectories while overlooking rare and informative events. Prioritized experience replay can assign greater importance to samples associated with high prediction error, unexpected outcomes, novelty, uncertainty, failure, successful recovery, or significant policy improvement. The replay process then focuses learning resources on experiences with greater potential value.

Priority alone is insufficient because highly unusual experiences can dominate learning if repeatedly sampled. Replay systems therefore need mechanisms that balance novelty with representativeness. A useful buffer should contain routine behavior, difficult cases, failures, recoveries, environmental diversity, and multiple task conditions. Balanced sampling helps the model improve robustness without becoming excessively specialized toward rare events that do not represent normal fleet operation.

Cross-robot replay introduces compatibility challenges when experiences originate from heterogeneous robots. An action generated by a wheeled AMR may not have the same meaning for a quadruped, manipulator, humanoid, or UAV. Direct replay may therefore be limited to compatible embodiments, while higher-level information such as goals, semantic states, object relationships, rewards, task phases, or outcomes can be transformed into shared representations for broader reuse.

Policy differences also affect replay quality. Experiences stored in the buffer may have been generated by older policies, different robot configurations, or different exploration strategies. As fleet policies evolve, historical trajectories can become increasingly different from current behavior. Off-policy learning methods can use such data, but policy version information and behavior-policy metadata are important for determining how historical experience should influence current learning.

This creates the problem of replay staleness. Old experience is not automatically useless because it may contain rare and valuable knowledge, but environmental conditions or robot capabilities may have changed since collection. Timestamp information, model versions, environment metadata, recency weighting, and periodic re-evaluation can help distinguish enduring knowledge from experiences that no longer accurately represent current operating conditions.

Replay can also support cooperative multi-agent learning by preserving joint trajectories. Instead of storing each robot\'s transition independently, the system can retain synchronized observations, actions, rewards, messages, and outcomes from multiple agents participating in the same event. These joint experiences help learners analyze coordination, congestion, task handoffs, cooperative transport, formation behavior, and other outcomes that depend on interactions among robots.

Failure and recovery replay provides a particularly important mechanism for improving fleet resilience. When one robot becomes trapped, loses localization, fails a manipulation attempt, encounters an unexpected obstacle, or requires human intervention, the complete episode can be preserved. If a successful recovery follows, the transition from failure to recovery becomes reusable knowledge that can prepare other robots for similar operational disruptions.

Simulation and real-world replay can complement each other. Simulation can generate large numbers of diverse experiences, including dangerous or unusual situations that should not be intentionally reproduced with physical robots. Real-world trajectories provide evidence about actual sensor noise, hardware variation, human interaction, and environmental complexity. Replay buffers can combine both sources while maintaining metadata that identifies their origin and reliability.

Data quality and provenance remain essential because incorrect experiences can contaminate learning. Sensor faults, corrupted timestamps, inaccurate localization, software errors, or poorly calibrated hardware may produce misleading trajectories. Replay pipelines should preserve source identity, confidence, sensor status, policy version, and validation information so that unreliable experiences can be filtered, down-weighted, isolated, or investigated before they influence fleet models.

Storage management becomes important as deployment scales. A large fleet can generate far more experience than can be retained indefinitely. Replay systems may compress observations, retain representative episodes, remove redundant samples, preserve rare events, or maintain summaries of older experience. The objective is not to store everything, but to maintain a compact memory that represents the most useful history of collective physical interaction.

Experience replay across robots ultimately creates a form of collective memory for Physical AI. Every robot can contribute episodes to a shared learning resource, while future robots can learn from experiences they did not personally generate. Combined with shared experience, CTDE, multi-agent reinforcement learning, distributed updates, policy sharing, and continual learning, cross-robot replay transforms fleet history into reusable knowledge that progressively improves collective behavior.

로봇 간 경험 재현(Experience Replay Across Robots)은 개별 강화학습(Reinforcement Learning)의 리플레이 메모리(Replay Memory) 개념을 플릿 수준의 공유 학습 과정으로 확장한다. 각 로봇이 자신의 운영에서 생성한 궤적만으로 학습하는 대신, 여러 로봇에서 수집한 경험을 저장하고 선택하여 이후의 학습에서 재사용할 수 있다. 이를 통해 하나의 로봇이 한 번 생성한 물리적 상호작용 경험이 더 넓은 다중 로봇 시스템의 학습에 반복적으로 기여할 수 있다.

로봇 경험(Robot Experience)은 관측(Observation), 상태(State), 행동(Action), 보상(Reward), 다음 상태(Next State), 작업 결과(Task Outcome), 통신 이벤트(Communication Event), 실패, 개입(Intervention), 맥락 메타데이터(Contextual Metadata)를 포함할 수 있다. 여러 로봇의 경험을 결합하면 리플레이 시스템(Replay System)은 단순한 메모리 버퍼(Memory Buffer)를 넘어선다. 이는 서로 다른 에이전트가 다양한 환경 조건, 체화(Embodiment), 정책(Policy), 작업, 운영 제약에서 어떻게 행동했는지를 기록하는 분산형 경험 저장소가 된다.

로봇 간 리플레이(Cross-Robot Replay)의 주요 장점은 데이터 효율성(Data Efficiency)을 향상시키는 것이다. 물리적 로봇 경험을 수집하려면 시간, 에너지, 하드웨어 수명, 인간 감독, 운영 자원이 소모되기 때문에 높은 비용이 발생한다. 이전에 수집한 궤적을 재사용하면 학습 알고리즘이 기존 상호작용에서 추가적인 가치를 추출할 수 있다. 따라서 하나의 로봇이 경험한 어려운 상황이 동일한 상황을 직접 경험하지 않은 다른 로봇의 정책 향상에도 기여할 수 있다.

경험 다양성(Experience Diversity)은 또 다른 주요 장점이다. 개별 로봇은 일반적으로 전체 환경 분포(Environment Distribution)의 제한된 영역에서 운영된다. 하나의 로봇은 혼잡한 통로를 경험하고, 다른 로봇은 미끄러운 지형을 경험하며, 또 다른 로봇은 특이한 객체나 통신 실패를 경험할 수 있다. 이러한 경험을 결합하면 학습 분포가 확장되어 개별 로봇의 제한된 운영 이력을 넘어 일반화할 수 있는 행동을 모델이 학습하는 데 도움이 된다.

리플레이는 희귀 사건(Rare Event)을 학습할 때 특히 가치가 높다. 성공적인 일상 운영 데이터는 플릿 데이터셋(Fleet Dataset)의 대부분을 차지할 수 있지만 충돌, 위치추정 실패(Localization Failure), 비정상적인 장애물, 파지 실패(Grasp Failure), 통신 손실, 비상 정지(Emergency Stop), 복구 행동(Recovery Behavior)은 상대적으로 드물게 발생한다. 이러한 희귀 에피소드를 보존하고 적절한 우선순위로 반복 학습하면 최초 사건이 발생한 이후에도 플릿이 지속적으로 해당 경험으로부터 학습할 수 있다.

공유 리플레이 버퍼(Shared Replay Buffer)는 중앙집중식(Centralized), 계층적(Hierarchical), 분산형(Distributed) 구조로 구성할 수 있다. 중앙 저장소는 전체 플릿에서 선택된 궤적을 수집할 수 있으며, 사이트 수준 버퍼(Site-Level Buffer)는 특정 시설과 관련된 경험을 보존할 수 있다. 개별 로봇도 로컬 버퍼(Local Buffer)를 유지하면서 선택된 에피소드를 주변 에이전트와 교환할 수 있다. 하이브리드 아키텍처(Hybrid Architecture)는 대역폭, 저장 용량, 프라이버시, 운영 요구사항에 따라 이러한 구조를 결합할 수 있다.

모든 경험을 동일한 확률로 재현할 필요는 없다. 균일 샘플링(Uniform Sampling)은 단순하지만 일반적이고 정보 가치가 낮은 궤적을 반복적으로 선택하면서 희귀하고 유용한 사건을 놓칠 수 있다. 우선순위 경험 재현(Prioritized Experience Replay)은 높은 예측 오류(Prediction Error), 예상하지 못한 결과, 새로움(Novelty), 불확실성(Uncertainty), 실패, 성공적인 복구 또는 상당한 정책 향상과 관련된 샘플에 더 높은 중요도를 부여할 수 있다. 이를 통해 리플레이 과정은 잠재적 가치가 높은 경험에 학습 자원을 집중할 수 있다.

그러나 매우 특이한 경험이 반복적으로 샘플링되면 학습을 지나치게 지배할 수 있기 때문에 우선순위만으로는 충분하지 않다. 따라서 리플레이 시스템은 새로움과 대표성(Representativeness)의 균형을 유지하는 메커니즘이 필요하다. 유용한 버퍼는 일상적인 행동, 어려운 사례, 실패, 복구, 환경 다양성, 다양한 작업 조건을 함께 포함해야 한다. 균형 샘플링(Balanced Sampling)은 정상적인 플릿 운영을 대표하지 않는 희귀 사건에 모델이 지나치게 특화되는 것을 방지하면서 강건성(Robustness)을 향상시키는 데 도움을 준다.

로봇 간 리플레이는 서로 다른 이기종 로봇(Heterogeneous Robots)에서 경험이 생성되는 경우 호환성 문제(Compatibility Challenge)를 발생시킨다. 바퀴형 자율이동로봇(AMR)이 생성한 행동은 4족 보행 로봇(Quadruped), 매니퓰레이터(Manipulator), 휴머노이드(Humanoid), 무인항공기(UAV)에서 동일한 의미를 갖지 않을 수 있다. 따라서 직접적인 리플레이는 호환 가능한 체화로 제한하고, 목표, 의미론적 상태(Semantic State), 객체 관계, 보상, 작업 단계(Task Phase), 결과와 같은 상위 수준 정보는 공유 표현(Shared Representation)으로 변환하여 더 광범위하게 재사용할 수 있다.

정책 차이(Policy Difference) 역시 리플레이 품질에 영향을 준다. 버퍼에 저장된 경험은 이전 정책, 다른 로봇 구성 또는 서로 다른 탐색 전략(Exploration Strategy)을 이용하여 생성되었을 수 있다. 플릿 정책이 발전함에 따라 과거 궤적은 현재 행동과 점차 달라질 수 있다. 오프폴리시 학습(Off-Policy Learning)은 이러한 데이터를 활용할 수 있지만, 과거 경험이 현재 학습에 어느 정도 영향을 미쳐야 하는지를 결정하기 위해 정책 버전 정보(Policy Version Information)와 행동 정책 메타데이터(Behavior-Policy Metadata)가 중요하다.

이는 리플레이 노후화(Replay Staleness) 문제로 이어진다. 오래된 경험이라고 해서 자동으로 쓸모없어지는 것은 아니며 희귀하고 가치 있는 지식을 포함할 수 있지만, 경험이 수집된 이후 환경 조건이나 로봇 역량이 변경되었을 수도 있다. 타임스탬프(Timestamp), 모델 버전(Model Version), 환경 메타데이터(Environment Metadata), 최신성 가중치(Recency Weighting), 주기적 재평가(Periodic Re-Evaluation)를 활용하면 지속적으로 유효한 지식과 현재 운영 조건을 더 이상 정확하게 나타내지 못하는 경험을 구분할 수 있다.

리플레이는 공동 궤적(Joint Trajectory)을 보존함으로써 협력적 다중 에이전트 학습(Cooperative Multi-Agent Learning)도 지원할 수 있다. 각 로봇의 상태 전이(Transition)를 독립적으로 저장하는 대신 동일한 사건에 참여한 여러 에이전트의 동기화된 관측, 행동, 보상, 메시지, 결과를 함께 보존할 수 있다. 이러한 공동 경험은 로봇 간 상호작용에 따라 결과가 달라지는 협조(Coordination), 혼잡, 작업 인계(Task Handoff), 협력 운송(Cooperative Transport), 대형 행동(Formation Behavior)을 학습 시스템이 분석하는 데 도움을 준다.

실패 및 복구 재현(Failure and Recovery Replay)은 플릿의 회복탄력성(Resilience)을 향상시키는 데 특히 중요한 메커니즘을 제공한다. 하나의 로봇이 갇히거나, 위치추정을 상실하거나, 조작 작업에 실패하거나, 예상하지 못한 장애물을 만나거나, 인간의 개입을 필요로 했을 경우 전체 에피소드를 보존할 수 있다. 이후 성공적인 복구가 이루어졌다면 실패에서 복구로 전환되는 과정 자체가 재사용 가능한 지식이 되어 다른 로봇이 유사한 운영 장애에 대비하도록 할 수 있다.

시뮬레이션 리플레이(Simulation Replay)와 실제 환경 리플레이(Real-World Replay)는 서로 보완적으로 활용할 수 있다. 시뮬레이션은 실제 로봇으로 의도적으로 재현해서는 안 되는 위험하거나 특이한 상황을 포함하여 대량의 다양한 경험을 생성할 수 있다. 실제 환경의 궤적은 현실적인 센서 노이즈, 하드웨어 편차, 인간 상호작용, 환경 복잡성에 대한 증거를 제공한다. 리플레이 버퍼는 데이터의 출처와 신뢰성을 식별하는 메타데이터를 유지하면서 두 종류의 경험을 함께 활용할 수 있다.

잘못된 경험이 학습을 오염시킬 수 있기 때문에 데이터 품질(Data Quality)과 출처 추적(Provenance)은 필수적이다. 센서 고장, 손상된 타임스탬프, 부정확한 위치추정, 소프트웨어 오류, 잘못 캘리브레이션된 하드웨어는 오해를 유발하는 궤적을 생성할 수 있다. 따라서 리플레이 파이프라인(Replay Pipeline)은 출처 식별정보, 신뢰도(Confidence), 센서 상태, 정책 버전, 검증 정보를 유지하여 신뢰할 수 없는 경험이 플릿 모델에 영향을 주기 전에 필터링, 가중치 감소, 격리 또는 분석될 수 있도록 해야 한다.

배포 규모가 증가하면 저장장치 관리(Storage Management)가 중요해진다. 대규모 플릿은 무기한 보존할 수 있는 양보다 훨씬 많은 경험을 생성할 수 있다. 리플레이 시스템은 관측 데이터를 압축하거나, 대표적인 에피소드를 유지하거나, 중복 샘플을 제거하고, 희귀 사건을 보존하거나, 오래된 경험의 요약 정보를 유지할 수 있다. 목표는 모든 데이터를 저장하는 것이 아니라 집단적인 물리 상호작용의 이력 가운데 학습에 가장 유용한 부분을 대표하는 압축된 메모리(Compact Memory)를 유지하는 것이다.

궁극적으로 로봇 간 경험 재현(Experience Replay Across Robots)은 피지컬 AI(Physical AI)를 위한 일종의 집단 기억(Collective Memory)을 형성한다. 모든 로봇은 공유 학습 자원에 에피소드를 제공할 수 있으며, 미래의 로봇은 자신이 직접 생성하지 않은 경험으로부터 학습할 수 있다. 공유 경험(Shared Experience), 중앙집중식 학습과 분산 실행(CTDE), 다중 에이전트 강화학습(Multi-Agent Reinforcement Learning), 분산 업데이트(Distributed Updates), 정책 공유(Policy Sharing), 지속학습(Continual Learning)과 결합하면 로봇 간 리플레이는 플릿의 운영 이력(Fleet History)을 집단 행동을 지속적으로 향상시키는 재사용 가능한 지식으로 변환한다.

##  

## 05.10. Cross Robot Transfer Learning

![](images/image12.png){width="7.268055555555556in" height="7.268055555555556in"}

Cross-robot transfer learning enables knowledge acquired by one robot, robot group, or deployment environment to accelerate learning on another robot. Instead of treating every new platform or mission as an independent learning problem, previously learned representations, models, policies, skills, and experience can provide a starting point. The objective is to reuse transferable knowledge while adapting those elements that depend on embodiment, sensors, tasks, or environments.

The simplest transfer occurs between robots with similar hardware and operating conditions. A navigation model trained on one AMR can initialize another robot using comparable sensors, kinematics, and control interfaces. The receiving robot may require only limited local adaptation rather than complete retraining. This reduces data collection, computation, deployment time, and the amount of risky exploration required in the physical environment.

Transfer becomes more challenging as differences between source and target robots increase. Robots may differ in wheel configuration, manipulators, camera placement, LiDAR characteristics, payload, control frequency, dynamics, or action spaces. A policy expressed directly as motor commands may therefore transfer poorly. Cross-robot learning must identify which parts of knowledge are platform-independent and which must remain specific to the target embodiment.

Representation learning provides an important mechanism for achieving this separation. Instead of transferring raw sensor values or actuator commands, robots can share latent representations describing objects, geometry, traversability, goals, task phases, spatial relationships, affordances, or expected outcomes. A common representation allows physically different robots to reason about similar situations while their local controllers translate abstract decisions into embodiment-specific actions.

Transfer can occur at multiple levels of the learning architecture. Low-level transfer may reuse perception features, calibration priors, motion representations, or controller parameters between similar platforms. Intermediate transfer can share navigation concepts, manipulation primitives, object representations, or recovery skills. Higher-level transfer can reuse task strategies, semantic knowledge, planning rules, world knowledge, and coordination patterns across substantially different robot embodiments.

Policy transfer is useful when the source policy already captures behavior relevant to the target task. The target robot can initialize its policy from selected source parameters and then fine-tune them using local experience. When direct parameter reuse is inappropriate, knowledge distillation can train a target policy to reproduce useful behavior from a source model while respecting a different architecture, observation space, computational budget, or action interface.

Skill transfer offers greater flexibility because skills can be represented above the actuator level. Concepts such as navigate-to-goal, inspect-object, follow-agent, explore-region, recover-localization, transport-object, or maintain-formation describe behavioral objectives rather than exact motor commands. Different robots can therefore share the same skill semantics while implementing execution through their own planners, controllers, sensors, and physical capabilities.

Task transfer allows knowledge learned for one objective to accelerate another related objective. Experience from autonomous navigation may support inspection, delivery, patrol, or search tasks because these missions share localization, obstacle avoidance, map understanding, and motion planning capabilities. Transfer learning can preserve these reusable components while adapting task-specific policies, rewards, decision layers, or skill compositions for the new mission.

Environmental transfer addresses differences between deployment domains. A robot trained in one warehouse may be transferred to another facility with different layouts, lighting, traffic patterns, floor surfaces, or objects. The target robot should retain generally useful representations while adapting to local conditions. Domain adaptation, fine-tuning, feature alignment, and environment-specific parameters can reduce the need to relearn capabilities that remain valid across sites.

Positive transfer occurs when reused knowledge improves target learning or performance, but transfer is not always beneficial. Negative transfer can occur when source knowledge contains assumptions that are inappropriate for the target robot or environment. A policy optimized for smooth indoor floors, for example, may provide misleading behavior for rough outdoor terrain. Transfer mechanisms must therefore estimate compatibility rather than assuming that previously learned knowledge is universally useful.

Compatibility assessment can consider embodiment, sensor configuration, action space, task similarity, environmental context, model architecture, and historical performance. Metadata associated with policies, skills, datasets, and experiences can help determine whether direct reuse, partial transfer, transformation, or complete rejection is appropriate. Transfer then becomes a selective knowledge-routing process rather than indiscriminate copying between robots.

Cross-robot transfer also benefits from modular architectures. A shared perception or world-model backbone can capture broadly useful knowledge while robot-specific adapters, policy heads, or controllers represent local differences. When a new robot joins the fleet, it can inherit the common backbone and train only a relatively small set of specialized parameters. This approach supports rapid onboarding while preserving embodiment-specific behavior.

Experience can be transferred even when models cannot. Trajectories generated by one robot may provide useful supervision, goals, semantic relationships, failure cases, or task outcomes for another platform. Cross-robot experience replay can transform compatible portions of historical trajectories into shared representations. The target robot can then learn from events it never physically experienced, increasing data efficiency and expanding its operational knowledge.

Simulation can provide an intermediate transfer layer between heterogeneous robots. Source experiences can be reconstructed or approximated in simulation, where the target embodiment attempts equivalent tasks using its own dynamics and sensors. This allows knowledge to be translated before physical deployment. Simulation can also test whether transferred policies or skills remain safe and effective before they are adapted on real hardware.

Safety validation is necessary because transferred knowledge may fail in ways that were absent on the source platform. Differences in braking distance, payload, stability, reach, sensor blind spots, or actuator limits can turn previously successful behavior into unsafe behavior. Simulation, digital twins, controlled testing, runtime constraints, staged deployment, and rollback mechanisms should therefore accompany transfer into operational Physical AI systems.

At fleet scale, transfer learning creates a knowledge network in which learning performed by one robot can reduce the learning burden of future robots. New platforms begin from accumulated fleet knowledge instead of an empty model, contribute their own adaptations, and return useful improvements to the shared knowledge base. The process gradually increases the diversity and maturity of transferable representations, policies, skills, and experience.

Cross-robot transfer learning therefore connects individual adaptation with collective capability accumulation. Shared experience provides the source material, experience replay preserves useful history, policy and skill sharing exposes reusable behavior, and distributed learning propagates improvements. Together, these mechanisms allow a heterogeneous Physical AI fleet to convert knowledge acquired across robots, tasks, environments, and missions into progressively broader collective intelligence.

로봇 간 전이학습(Cross-Robot Transfer Learning)은 하나의 로봇, 로봇 그룹 또는 배포 환경에서 획득한 지식을 다른 로봇의 학습을 가속하는 데 활용할 수 있도록 한다. 새로운 플랫폼이나 임무를 매번 독립적인 학습 문제로 취급하는 대신, 이전에 학습된 표현(Representation), 모델(Model), 정책(Policy), 기술(Skill), 경험(Experience)을 새로운 학습의 출발점으로 사용할 수 있다. 목표는 전이 가능한 지식을 재사용하면서 체화(Embodiment), 센서, 작업 또는 환경에 의존하는 요소만 적절하게 적응시키는 것이다.

가장 단순한 전이는 유사한 하드웨어와 운영 조건을 가진 로봇 사이에서 이루어진다. 하나의 자율이동로봇(Autonomous Mobile Robot, AMR)에서 학습된 내비게이션 모델(Navigation Model)을 유사한 센서, 운동학(Kinematics), 제어 인터페이스(Control Interface)를 사용하는 다른 로봇의 초기 모델로 활용할 수 있다. 수신 로봇은 완전한 재학습 대신 제한적인 로컬 적응(Local Adaptation)만 수행하면 될 수 있다. 이를 통해 데이터 수집, 연산량, 배포 시간, 실제 물리 환경에서 필요한 위험한 탐색의 양을 줄일 수 있다.

소스 로봇(Source Robot)과 타깃 로봇(Target Robot)의 차이가 커질수록 전이는 더욱 어려워진다. 로봇은 휠 구성, 매니퓰레이터(Manipulator), 카메라 배치, 라이다(LiDAR) 특성, 적재량(Payload), 제어 주기(Control Frequency), 동역학(Dynamics), 행동 공간(Action Space)에서 서로 다를 수 있다. 따라서 모터 명령으로 직접 표현된 정책은 전이 성능이 낮을 수 있다. 로봇 간 학습은 어떤 지식이 플랫폼 독립적이며 어떤 지식이 타깃 체화에 특화되어야 하는지를 식별해야 한다.

표현학습(Representation Learning)은 이러한 분리를 구현하기 위한 중요한 메커니즘을 제공한다. 원시 센서 값이나 액추에이터 명령을 직접 전이하는 대신 로봇은 객체, 기하 구조(Geometry), 주행 가능성(Traversability), 목표, 작업 단계(Task Phase), 공간 관계(Spatial Relationship), 어포던스(Affordance), 예상 결과를 설명하는 잠재 표현(Latent Representation)을 공유할 수 있다. 공통 표현(Common Representation)을 사용하면 물리적으로 서로 다른 로봇이 유사한 상황을 공통적으로 추론하면서 각 로봇의 로컬 제어기가 추상적인 의사결정을 체화 특화 행동으로 변환할 수 있다.

전이는 학습 아키텍처의 여러 수준에서 이루어질 수 있다. 저수준 전이(Low-Level Transfer)는 유사한 플랫폼 사이에서 인식 특징(Perception Feature), 캘리브레이션 사전정보(Calibration Prior), 모션 표현(Motion Representation), 제어기 파라미터를 재사용할 수 있다. 중간 수준 전이는 내비게이션 개념, 조작 프리미티브(Manipulation Primitive), 객체 표현, 복구 기술(Recovery Skill)을 공유할 수 있다. 상위 수준 전이(High-Level Transfer)는 상당히 다른 로봇 체화 사이에서도 작업 전략, 의미론적 지식(Semantic Knowledge), 계획 규칙(Planning Rule), 월드 지식(World Knowledge), 협조 패턴(Coordination Pattern)을 재사용할 수 있다.

정책 전이(Policy Transfer)는 소스 정책이 이미 타깃 작업과 관련된 행동을 포함하고 있을 때 유용하다. 타깃 로봇은 선택된 소스 파라미터로 자신의 정책을 초기화한 후 로컬 경험을 이용하여 미세조정(Fine-Tuning)할 수 있다. 직접적인 파라미터 재사용이 적절하지 않은 경우에는 지식 증류(Knowledge Distillation)를 통해 서로 다른 아키텍처, 관측 공간(Observation Space), 연산 자원 또는 행동 인터페이스를 사용하는 타깃 정책이 소스 모델의 유용한 행동을 재현하도록 학습할 수 있다.

기술 전이(Skill Transfer)는 액추에이터 수준보다 높은 수준에서 기술을 표현할 수 있기 때문에 더 높은 유연성을 제공한다. 목표 지점 이동(Navigate-to-Goal), 객체 검사(Inspect-Object), 에이전트 추종(Follow-Agent), 영역 탐색(Explore-Region), 위치추정 복구(Recover-Localization), 객체 운송(Transport-Object), 대형 유지(Maintain-Formation)와 같은 개념은 정확한 모터 명령이 아니라 행동 목표를 설명한다. 따라서 서로 다른 로봇이 동일한 기술 의미론(Skill Semantics)을 공유하면서 각자의 플래너(Planner), 제어기, 센서, 물리적 역량을 통해 실행할 수 있다.

작업 전이(Task Transfer)는 하나의 목표를 위해 학습된 지식을 관련된 다른 목표의 학습을 가속하는 데 활용한다. 자율주행 내비게이션(Autonomous Navigation) 경험은 검사, 배송, 순찰, 탐색 작업을 지원할 수 있는데, 이러한 임무가 위치추정(Localization), 장애물 회피(Obstacle Avoidance), 지도 이해(Map Understanding), 모션 계획(Motion Planning)과 같은 공통 역량을 공유하기 때문이다. 전이학습은 이러한 재사용 가능한 구성요소를 유지하면서 새로운 임무에 필요한 작업 특화 정책, 보상, 의사결정 계층 또는 기술 조합만 적응시킬 수 있다.

환경 전이(Environmental Transfer)는 서로 다른 배포 도메인(Deployment Domain) 사이의 차이를 다룬다. 하나의 창고에서 학습된 로봇을 서로 다른 레이아웃, 조명, 교통 패턴, 바닥 표면 또는 객체를 가진 다른 시설로 전이할 수 있다. 타깃 로봇은 일반적으로 유용한 표현을 유지하면서 로컬 조건에 적응해야 한다. 도메인 적응(Domain Adaptation), 미세조정, 특징 정렬(Feature Alignment), 환경 특화 파라미터(Environment-Specific Parameter)를 활용하면 사이트 간에도 유효한 역량을 처음부터 다시 학습해야 하는 필요성을 줄일 수 있다.

재사용된 지식이 타깃의 학습이나 성능을 향상시키는 경우를 긍정적 전이(Positive Transfer)라고 하지만 전이가 항상 유익한 것은 아니다. 소스 지식이 타깃 로봇이나 환경에 적절하지 않은 가정을 포함하고 있으면 부정적 전이(Negative Transfer)가 발생할 수 있다. 예를 들어 매끄러운 실내 바닥에 최적화된 정책은 거친 실외 지형에서 잘못된 행동을 유도할 수 있다. 따라서 전이 메커니즘은 이전에 학습된 지식이 보편적으로 유용하다고 가정하기보다 호환성(Compatibility)을 평가해야 한다.

호환성 평가(Compatibility Assessment)는 체화, 센서 구성, 행동 공간, 작업 유사성(Task Similarity), 환경 맥락(Environmental Context), 모델 아키텍처(Model Architecture), 과거 성능을 고려할 수 있다. 정책, 기술, 데이터셋, 경험과 함께 저장된 메타데이터(Metadata)를 이용하면 직접 재사용, 부분 전이(Partial Transfer), 변환(Transformation), 완전한 거부 중 어떤 방법이 적절한지를 판단할 수 있다. 따라서 전이는 로봇 사이에서 지식을 무차별적으로 복사하는 과정이 아니라 선택적 지식 라우팅(Selective Knowledge Routing) 과정이 된다.

로봇 간 전이학습은 모듈형 아키텍처(Modular Architecture)를 통해서도 효과적으로 구현할 수 있다. 공유 인식 또는 월드 모델 백본(Shared Perception or World-Model Backbone)은 광범위하게 활용할 수 있는 지식을 학습하고, 로봇 특화 어댑터(Robot-Specific Adapter), 정책 헤드(Policy Head), 제어기(Controller)는 로컬 차이를 표현할 수 있다. 새로운 로봇이 플릿에 참여하면 공통 백본을 상속하고 상대적으로 작은 규모의 특화 파라미터만 학습할 수 있다. 이러한 접근법은 체화 특화 행동을 유지하면서 빠른 로봇 온보딩(Robot Onboarding)을 지원한다.

모델 자체를 직접 전이할 수 없는 경우에도 경험(Experience)은 전이할 수 있다. 하나의 로봇이 생성한 궤적(Trajectory)은 다른 플랫폼에 유용한 지도 정보(Supervision), 목표, 의미론적 관계, 실패 사례 또는 작업 결과를 제공할 수 있다. 로봇 간 경험 재현(Cross-Robot Experience Replay)은 과거 궤적에서 호환 가능한 부분을 공유 표현으로 변환할 수 있다. 타깃 로봇은 자신이 물리적으로 직접 경험하지 않은 사건에서도 학습할 수 있어 데이터 효율성과 운영 지식의 범위를 확대할 수 있다.

시뮬레이션(Simulation)은 이기종 로봇 사이의 중간 전이 계층(Intermediate Transfer Layer)을 제공할 수 있다. 소스 경험을 시뮬레이션에서 재구성하거나 근사하고, 타깃 체화가 자신의 동역학과 센서를 이용하여 동일하거나 유사한 작업을 수행하도록 할 수 있다. 이를 통해 실제 물리적 배포 전에 지식을 변환할 수 있다. 또한 시뮬레이션을 활용하면 전이된 정책이나 기술이 실제 하드웨어에서 적응되기 전에 안전하고 효과적인지를 검증할 수 있다.

전이된 지식은 소스 플랫폼에서 나타나지 않았던 방식으로 실패할 수 있기 때문에 안전 검증(Safety Validation)이 필요하다. 제동 거리(Braking Distance), 적재량, 안정성, 도달 범위(Reach), 센서 사각지대(Sensor Blind Spot), 액추에이터 한계의 차이로 인해 이전에는 성공적이었던 행동이 위험한 행동으로 변할 수 있다. 따라서 운영 피지컬 AI(Physical AI) 시스템으로 지식을 전이할 때는 시뮬레이션, 디지털 트윈(Digital Twin), 통제된 시험, 런타임 제약(Runtime Constraint), 단계적 배포(Staged Deployment), 롤백(Rollback) 메커니즘을 함께 적용해야 한다.

플릿 규모(Fleet Scale)에서 전이학습은 하나의 로봇에서 수행된 학습이 미래 로봇의 학습 부담을 줄일 수 있는 지식 네트워크(Knowledge Network)를 형성한다. 새로운 플랫폼은 빈 모델에서 시작하는 대신 축적된 플릿 지식(Fleet Knowledge)을 기반으로 시작하고, 자체적인 적응 결과를 추가한 후 유용한 개선 사항을 다시 공유 지식 기반(Shared Knowledge Base)에 제공한다. 이러한 과정은 전이 가능한 표현, 정책, 기술, 경험의 다양성과 성숙도를 점진적으로 향상시킨다.

따라서 로봇 간 전이학습(Cross-Robot Transfer Learning)은 개별 적응(Individual Adaptation)을 집단 역량 축적(Collective Capability Accumulation)과 연결한다. 공유 경험(Shared Experience)은 전이를 위한 원천 자료를 제공하고, 경험 재현(Experience Replay)은 유용한 이력을 보존하며, 정책 및 기술 공유(Policy and Skill Sharing)는 재사용 가능한 행동을 제공하고, 분산 학습(Distributed Learning)은 개선된 지식을 확산한다. 이러한 메커니즘을 결합하면 이기종 피지컬 AI 플릿(Heterogeneous Physical AI Fleet)은 서로 다른 로봇, 작업, 환경, 임무에서 획득한 지식을 점차 더 광범위한 집단 지능(Collective Intelligence)으로 발전시킬 수 있다.

##  

## 05.11. Catastrophic Interference and Knowledge Conflict

![](images/image13.png){width="7.268055555555556in" height="7.268055555555556in"}

Catastrophic interference occurs when learning from new robot experiences modifies a model in ways that damage knowledge acquired from earlier tasks, environments, or robots. In collective learning, this problem extends beyond individual forgetting because updates produced by one robot can propagate through shared models and influence an entire fleet. A useful update for one operating condition may therefore unintentionally degrade capabilities that were previously reliable elsewhere.

The underlying difficulty comes from shared model parameters. Neural networks often reuse the same parameters and representations across perception, world modeling, planning, and control. When new gradients modify parameters that encode earlier capabilities, the optimization direction for new knowledge may conflict with the direction needed to preserve old knowledge. Sequential learning can consequently replace rather than accumulate useful information.

Knowledge conflict is broader than catastrophic forgetting because two experiences can both remain valid while recommending different behaviors. A robot operating on a slippery floor may learn a cautious motion policy, whereas another operating on a high-friction surface may learn aggressive acceleration. Neither experience is necessarily incorrect. The conflict appears when a collective learning system attempts to represent both context-dependent behaviors through the same parameters or policy.

The problem becomes more difficult in heterogeneous fleets because robots differ in embodiment, sensors, dynamics, payload, control interfaces, and operational objectives. Knowledge learned by an AMR, quadruped, UAV, manipulator, or humanoid may describe different relationships between observations and actions. Combining these experiences without recognizing embodiment context can create interference even when each robot\'s local knowledge is individually correct.

Environmental diversity creates another source of conflict. Policies learned in warehouses, factories, hospitals, outdoor terrain, or public environments may encode different assumptions about obstacles, people, surfaces, visibility, communication, and acceptable behavior. A collective model must distinguish knowledge that is universally transferable from knowledge that applies only under particular conditions. Otherwise, global aggregation can produce a policy that performs poorly everywhere.

Gradient conflict provides a practical way to understand interference during distributed learning. If updates from two robots point toward compatible parameter changes, aggregation can improve both capabilities. If their gradients oppose each other, improving one objective may increase the loss associated with another. Detecting gradient similarity, parameter sensitivity, or task-level performance changes can therefore help identify destructive interactions before updates are widely propagated.

Experience replay provides one defense against catastrophic interference. When a model learns from new fleet experience, representative historical episodes can be replayed alongside recent data. The learner is therefore reminded of behaviors that should remain functional while incorporating new knowledge. Rare failures, recovery episodes, safety-critical scenarios, and previously mastered tasks are particularly valuable because they can otherwise disappear from the current training distribution.

Replay must remain balanced because simply storing large quantities of historical data does not guarantee knowledge preservation. Routine experiences can dominate the buffer while rare but important capabilities receive insufficient rehearsal. Sampling strategies can preserve representative examples across tasks, robots, environments, failures, and historical model versions. The objective is to maintain a learning distribution that reflects both current adaptation needs and important past competence.

Parameter protection offers another approach. Parameters that are strongly associated with established capabilities can be identified and constrained against large changes during subsequent learning. Other parameters remain more plastic and can absorb new knowledge. This creates a stability-plasticity balance in which important existing behavior is protected without preventing the model from adapting to genuinely new operating conditions.

Parameter-efficient adaptation can reduce interference by limiting which parts of a large model are modified. Instead of fine-tuning an entire shared foundation model, robots can learn adapters, low-rank updates, specialized policy heads, prompts, or other compact modules. The common backbone remains relatively stable while local or task-specific knowledge is stored in smaller components, reducing the probability that one adaptation will damage unrelated fleet capabilities.

Modularity provides a stronger form of knowledge separation. Perception, navigation, manipulation, communication, recovery, and task-specific skills can be represented through partially independent modules rather than forcing all knowledge into a single parameter space. When conflicts occur, the system can preserve multiple specialized modules and select among them according to embodiment, environment, task, or context instead of averaging incompatible behaviors.

Context-aware routing is therefore important for resolving knowledge conflict. A fleet does not always need to determine that one policy is globally correct and another is wrong. Both may be retained and activated under different conditions. Metadata describing robot type, terrain, payload, sensor configuration, task, environment, model version, and confidence can help a routing mechanism select the most appropriate policy, adapter, skill, or memory for the current situation.

Conflict detection should occur before model updates become fleet-wide knowledge. Candidate updates can be evaluated against regression suites containing previously mastered tasks and safety-critical scenarios. If performance improves on the new task but declines substantially on established capabilities, the update indicates interference. Per-task metrics are therefore more informative than a single average score, which can hide severe degradation in a minority of important behaviors.

Knowledge provenance also helps determine how conflicts should be resolved. Every shared policy, skill, experience, or model update can retain information about which robot generated it, under what conditions, from which model version, and with what performance evidence. When contradictory knowledge appears, the system can examine its origin rather than blindly averaging it. Provenance turns conflicting updates into interpretable alternatives that can be compared and validated.

Some conflicts reflect outdated knowledge rather than true incompatibility. A route that was once safe may become blocked, a warehouse layout may change, or a sensor configuration may be replaced. Temporal information and revalidation are therefore necessary before protecting historical knowledge indefinitely. Continual learning must distinguish valuable long-term competence from obsolete assumptions, preserving the former while allowing the latter to be revised or removed.

Safety-critical knowledge deserves particularly strong protection. Collision avoidance, emergency stopping, human separation, actuator constraints, and validated recovery behavior should not be sacrificed simply because a new policy improves average task efficiency. Safety constraints can remain outside or above adaptive policies, while regression testing ensures that learning updates do not silently remove behaviors required for dependable physical operation.

At fleet scale, interference management becomes a form of knowledge governance. Distributed updates should not immediately become universal truth simply because they improved one robot. New knowledge can be classified, validated, replayed against historical experience, compared with existing policies, and either merged, specialized, quarantined, or rejected. Versioning and rollback ensure that harmful integration can be reversed after deployment.

The broader objective is to make collective learning cumulative rather than destructive. Shared experience, cross-robot transfer, distributed updates, and policy sharing increase the rate at which knowledge enters the fleet, but mechanisms for replay, parameter protection, modularity, contextual routing, provenance, validation, and rollback determine whether that knowledge can coexist. Managing catastrophic interference and knowledge conflict is therefore fundamental to building robot fleets that become more capable over time without repeatedly sacrificing what they have already learned.

치명적 간섭(Catastrophic Interference)은 새로운 로봇 경험을 학습하는 과정에서 모델이 변경되어 이전 작업, 환경 또는 로봇으로부터 획득한 지식이 손상되는 현상을 의미한다. 집단 학습(Collective Learning)에서는 하나의 로봇이 생성한 업데이트가 공유 모델(Shared Model)을 통해 전체 플릿(Fleet)에 전파될 수 있기 때문에 이 문제는 개별적인 망각보다 더 광범위하다. 따라서 특정 운영 조건에서는 유용한 업데이트가 다른 환경에서 이미 안정적으로 작동하던 역량을 의도하지 않게 저하시킬 수 있다.

근본적인 어려움은 공유 모델 파라미터(Shared Model Parameters)에서 발생한다. 신경망(Neural Network)은 인식(Perception), 월드 모델링(World Modeling), 계획(Planning), 제어(Control) 전반에서 동일한 파라미터와 표현(Representation)을 재사용하는 경우가 많다. 새로운 그래디언트(Gradient)가 기존 역량을 표현하는 파라미터를 변경하면 새로운 지식의 최적화 방향이 기존 지식을 유지하는 데 필요한 방향과 충돌할 수 있다. 결과적으로 순차 학습(Sequential Learning)은 유용한 정보를 축적하기보다 기존 정보를 새로운 정보로 대체할 수 있다.

지식 충돌(Knowledge Conflict)은 두 경험이 모두 유효하지만 서로 다른 행동을 권장할 수도 있다는 점에서 치명적 망각(Catastrophic Forgetting)보다 더 넓은 개념이다. 미끄러운 바닥에서 동작하는 로봇은 신중한 이동 정책을 학습할 수 있고, 마찰력이 높은 표면에서 동작하는 다른 로봇은 적극적인 가속 정책을 학습할 수 있다. 두 경험 중 어느 것도 반드시 잘못된 것은 아니다. 집단 학습 시스템이 이러한 상황 의존적 행동(Context-Dependent Behavior)을 동일한 파라미터나 정책으로 표현하려 할 때 충돌이 발생한다.

이기종 플릿(Heterogeneous Fleet)에서는 로봇의 체화(Embodiment), 센서, 동역학(Dynamics), 적재량(Payload), 제어 인터페이스(Control Interface), 운영 목표가 서로 다르기 때문에 문제가 더욱 어려워진다. 자율이동로봇(AMR), 4족 보행 로봇(Quadruped), 무인항공기(UAV), 매니퓰레이터(Manipulator), 휴머노이드(Humanoid)가 학습한 지식은 관측과 행동 사이의 서로 다른 관계를 나타낼 수 있다. 체화 맥락을 인식하지 않고 이러한 경험을 결합하면 각 로봇의 로컬 지식이 개별적으로는 올바르더라도 간섭이 발생할 수 있다.

환경 다양성(Environmental Diversity)은 또 다른 충돌 원인을 만든다. 창고, 공장, 병원, 실외 지형 또는 공공 환경에서 학습된 정책은 장애물, 사람, 표면, 가시성, 통신, 허용 가능한 행동에 대해 서로 다른 가정을 포함할 수 있다. 집단 모델(Collective Model)은 보편적으로 전이 가능한 지식과 특정 조건에서만 적용되는 지식을 구분해야 한다. 그렇지 않으면 전역 통합(Global Aggregation)을 통해 어디에서도 제대로 동작하지 않는 정책이 만들어질 수 있다.

그래디언트 충돌(Gradient Conflict)은 분산 학습(Distributed Learning) 과정에서 발생하는 간섭을 이해하는 실용적인 방법을 제공한다. 두 로봇의 업데이트가 서로 호환되는 파라미터 변경 방향을 가리킨다면 통합을 통해 두 역량을 모두 향상시킬 수 있다. 반대로 그래디언트가 서로 반대 방향을 가리키면 하나의 목표를 개선하는 과정에서 다른 목표의 손실(Loss)이 증가할 수 있다. 따라서 그래디언트 유사성(Gradient Similarity), 파라미터 민감도(Parameter Sensitivity), 작업 수준 성능 변화를 탐지하면 업데이트가 광범위하게 전파되기 전에 파괴적인 상호작용을 식별하는 데 도움이 된다.

경험 재현(Experience Replay)은 치명적 간섭에 대응하기 위한 하나의 방어 방법을 제공한다. 모델이 새로운 플릿 경험을 학습할 때 대표적인 과거 에피소드(Historical Episode)를 최근 데이터와 함께 다시 학습할 수 있다. 이를 통해 새로운 지식을 통합하면서도 유지해야 하는 기존 행동을 학습기에 다시 상기시킬 수 있다. 희귀 실패(Rare Failure), 복구 에피소드(Recovery Episode), 안전 중요 시나리오(Safety-Critical Scenario), 이전에 숙달한 작업은 현재 학습 분포에서 사라질 가능성이 있기 때문에 특히 중요하다.

과거 데이터를 대량으로 저장하는 것만으로 지식 보존이 보장되는 것은 아니므로 리플레이(Replay)는 균형을 유지해야 한다. 일상적인 경험이 버퍼(Buffer)를 지배하면 드물지만 중요한 역량이 충분히 반복 학습되지 않을 수 있다. 샘플링 전략(Sampling Strategy)을 통해 작업, 로봇, 환경, 실패, 과거 모델 버전에 걸쳐 대표적인 사례를 유지할 수 있다. 목표는 현재의 적응 요구와 중요한 과거 역량을 모두 반영하는 학습 분포를 유지하는 것이다.

파라미터 보호(Parameter Protection)는 또 다른 접근법을 제공한다. 이미 확립된 역량과 강하게 연관된 파라미터를 식별하여 이후 학습에서 큰 변화가 발생하지 않도록 제한할 수 있다. 반면 다른 파라미터에는 더 높은 가소성(Plasticity)을 허용하여 새로운 지식을 받아들이도록 할 수 있다. 이를 통해 중요한 기존 행동을 보호하면서도 실제로 새로운 운영 조건에 적응할 수 있는 안정성-가소성 균형(Stability-Plasticity Balance)을 형성할 수 있다.

파라미터 효율적 적응(Parameter-Efficient Adaptation)은 대규모 모델에서 변경되는 부분을 제한함으로써 간섭을 줄일 수 있다. 전체 공유 파운데이션 모델(Shared Foundation Model)을 미세조정(Fine-Tuning)하는 대신 로봇은 어댑터(Adapter), 저랭크 업데이트(Low-Rank Update), 특화 정책 헤드(Specialized Policy Head), 프롬프트(Prompt) 또는 기타 소형 모듈을 학습할 수 있다. 공통 백본(Common Backbone)은 비교적 안정적으로 유지되고 로컬 또는 작업 특화 지식은 더 작은 구성요소에 저장되므로 하나의 적응 과정이 관련 없는 플릿 역량을 손상시킬 가능성을 줄일 수 있다.

모듈성(Modularity)은 더욱 강력한 형태의 지식 분리를 제공한다. 인식, 내비게이션, 조작(Manipulation), 통신, 복구, 작업 특화 기술(Task-Specific Skill)을 모든 지식이 하나의 파라미터 공간에 강제로 통합되도록 하는 대신 부분적으로 독립된 모듈로 표현할 수 있다. 충돌이 발생하면 시스템은 서로 호환되지 않는 행동을 평균화하는 대신 여러 전문화된 모듈(Specialized Module)을 보존하고 체화, 환경, 작업 또는 맥락에 따라 적절한 모듈을 선택할 수 있다.

따라서 상황 인식 라우팅(Context-Aware Routing)은 지식 충돌을 해결하는 데 중요하다. 플릿이 항상 하나의 정책은 전역적으로 옳고 다른 정책은 틀렸다고 결정할 필요는 없다. 두 정책을 모두 유지하면서 서로 다른 조건에서 활성화할 수 있다. 로봇 유형, 지형, 적재량, 센서 구성, 작업, 환경, 모델 버전, 신뢰도(Confidence)를 설명하는 메타데이터(Metadata)는 라우팅 메커니즘이 현재 상황에 가장 적절한 정책, 어댑터, 기술 또는 메모리를 선택하는 데 도움을 줄 수 있다.

충돌 탐지(Conflict Detection)는 모델 업데이트가 플릿 전체의 지식이 되기 전에 수행되어야 한다. 후보 업데이트(Candidate Update)는 이전에 숙달된 작업과 안전 중요 시나리오를 포함하는 회귀 시험 세트(Regression Suite)를 통해 평가할 수 있다. 새로운 작업의 성능은 향상되지만 기존 역량의 성능이 크게 감소한다면 해당 업데이트는 간섭을 발생시키고 있음을 의미한다. 따라서 소수의 중요한 행동에서 발생하는 심각한 성능 저하를 숨길 수 있는 하나의 평균 점수보다 작업별 성능 지표(Per-Task Metric)가 더 유용하다.

지식 출처 추적(Knowledge Provenance)은 충돌을 어떻게 해결해야 하는지를 판단하는 데에도 도움을 준다. 모든 공유 정책, 기술, 경험 또는 모델 업데이트는 어떤 로봇이 생성했는지, 어떤 조건에서 생성되었는지, 어떤 모델 버전을 기반으로 했는지, 어떤 성능 증거(Performance Evidence)를 가지고 있는지에 대한 정보를 유지할 수 있다. 서로 모순되는 지식이 나타나면 시스템은 이를 무조건 평균화하지 않고 각각의 출처를 분석할 수 있다. 출처 추적을 통해 충돌하는 업데이트를 비교하고 검증할 수 있는 해석 가능한 대안으로 관리할 수 있다.

일부 충돌은 실제적인 비호환성이 아니라 오래된 지식(Outdated Knowledge) 때문에 발생한다. 이전에는 안전했던 경로가 차단되거나, 창고 레이아웃이 변경되거나, 센서 구성이 교체될 수 있다. 따라서 과거 지식을 무기한 보호하기 전에 시간 정보(Temporal Information)와 재검증(Revalidation)이 필요하다. 지속학습(Continual Learning)은 가치 있는 장기 역량(Long-Term Competence)과 더 이상 유효하지 않은 가정을 구분하고, 전자는 보존하면서 후자는 수정하거나 제거할 수 있어야 한다.

안전 중요 지식(Safety-Critical Knowledge)은 특히 강력하게 보호되어야 한다. 충돌 회피(Collision Avoidance), 비상 정지(Emergency Stopping), 인간과의 안전거리(Human Separation), 액추에이터 제약(Actuator Constraint), 검증된 복구 행동은 새로운 정책이 평균적인 작업 효율을 향상시킨다는 이유만으로 희생되어서는 안 된다. 안전 제약은 적응형 정책(Adaptive Policy)의 외부 또는 상위 계층에서 유지할 수 있으며, 회귀 시험을 통해 학습 업데이트가 신뢰할 수 있는 물리적 운영에 필요한 행동을 조용히 제거하지 않는지 확인할 수 있다.

플릿 규모(Fleet Scale)에서 간섭 관리는 일종의 지식 거버넌스(Knowledge Governance)가 된다. 분산 업데이트(Distributed Update)가 하나의 로봇 성능을 개선했다는 이유만으로 즉시 보편적인 진실로 받아들여져서는 안 된다. 새로운 지식은 분류되고, 검증되고, 과거 경험과 함께 재현되며, 기존 정책과 비교된 후 통합(Merge), 전문화(Specialize), 격리(Quarantine) 또는 거부(Reject)될 수 있다. 버전 관리(Versioning)와 롤백(Rollback)은 배포 이후 유해한 통합이 발견될 경우 이를 되돌릴 수 있도록 한다.

더 넓은 목표는 집단 학습(Collective Learning)을 파괴적인 과정이 아니라 누적적인 과정(Cumulative Process)으로 만드는 것이다. 공유 경험(Shared Experience), 로봇 간 전이(Cross-Robot Transfer), 분산 업데이트, 정책 공유(Policy Sharing)는 플릿으로 새로운 지식이 유입되는 속도를 높이지만, 경험 재현, 파라미터 보호, 모듈성, 상황 인식 라우팅, 출처 추적, 검증, 롤백 메커니즘은 이러한 지식이 서로 공존할 수 있는지를 결정한다. 따라서 치명적 간섭과 지식 충돌(Catastrophic Interference and Knowledge Conflict)의 관리는 로봇 플릿이 이미 학습한 역량을 반복적으로 희생하지 않으면서 시간이 지날수록 더욱 지능적으로 발전하기 위한 핵심 기반이다.

##  

## 05.12. Collective Curriculum and Continual Learning

![](images/image14.png){width="7.268055555555556in" height="7.268055555555556in"}

Collective curriculum and continual learning organize fleet intelligence as a progressive learning process rather than a sequence of independent training episodes. A collective curriculum determines which tasks, environments, failures, and coordination problems robots should learn from and in what progression, while continual learning preserves useful knowledge as new experience arrives. Together, they enable a robot fleet to accumulate capabilities throughout its operational lifetime.

Traditional robot training often follows a fixed dataset and a predefined task distribution. Physical deployments are different because robots continuously encounter new layouts, objects, users, teammates, disturbances, and mission requirements. The learning problem therefore changes over time. A collective curriculum responds to this changing distribution by selecting experiences and training challenges according to fleet competence, uncertainty, operational importance, and emerging capability gaps.

Curriculum learning introduces complexity gradually so that previously acquired capabilities provide foundations for more difficult behaviors. A robot may first learn stable navigation in structured spaces, then operate around dynamic obstacles, coordinate with teammates, recover from localization failures, and eventually execute complex multi-robot missions. This progression reduces unnecessary difficulty during early learning while creating reusable knowledge for later stages.

At fleet scale, curriculum generation can use experience from many robots rather than relying on a single predetermined sequence. If several robots repeatedly fail in similar situations, those situations can receive greater training priority. Conversely, tasks that are already performed reliably across the fleet may require less training attention. The curriculum therefore evolves according to collective performance instead of remaining fixed throughout development and deployment.

A useful collective curriculum must balance difficulty, novelty, and relevance. Experiences that are too easy provide little learning value, while challenges far beyond current capability may generate unstable training or meaningless failures. Tasks near the boundary of existing competence often provide stronger learning signals. Novel situations can be introduced progressively while maintaining enough familiar experience to preserve previously mastered behavior.

Different robots do not necessarily require identical curricula. Heterogeneous embodiments may possess different sensors, mobility systems, manipulators, computational resources, and mission roles. An AMR may require advanced navigation and logistics curricula, while a quadruped focuses on terrain traversal and stability. Shared task abstractions can connect these specialized curricula while allowing each embodiment to progress according to its own capabilities.

Collective curricula can also include cooperative tasks whose difficulty depends on relationships among robots. Initial stages may involve simple task allocation or formation maintenance, followed by coordinated exploration, cooperative transport, congestion management, communication-constrained operation, and heterogeneous team missions. Learning increasingly complex interaction structures allows collective behavior to develop from simpler coordination primitives.

Continual learning provides the mechanism for integrating these successive experiences without repeatedly retraining the entire system from the beginning. As new tasks and environments appear, models adapt while retaining important previous capabilities. This requires managing the stability-plasticity balance: the system must remain sufficiently plastic to acquire new knowledge while remaining sufficiently stable to prevent destructive changes to established skills.

Experience replay is one important mechanism for maintaining this balance. New curriculum experiences can be mixed with representative historical episodes during training so that older competencies remain active. Replay buffers may preserve routine operations, rare failures, successful recoveries, safety-critical cases, and representative tasks from previous curriculum stages. The fleet can therefore rehearse important knowledge while progressing toward new capabilities.

Modular and parameter-efficient learning can further reduce interference. Shared perception or world-model components may remain relatively stable while adapters, policy heads, skill modules, or other specialized parameters are updated for new curriculum stages. This allows the system to add capabilities without modifying every parameter simultaneously and supports different learning paths for robots operating under different conditions.

Curriculum selection can be driven by uncertainty and learning progress. Situations in which the model shows high uncertainty may indicate knowledge gaps, while tasks showing rapid improvement may represent productive learning regions. Persistent failure without improvement may indicate that prerequisite skills are missing. The curriculum manager can respond by selecting intermediate tasks that bridge the gap between current competence and the desired capability.

Failures are therefore valuable curriculum signals rather than merely undesirable outcomes. A localization loss, navigation deadlock, failed grasp, communication breakdown, or coordination error can reveal where the fleet lacks knowledge. Once detected and validated, these cases can be converted into replay episodes, simulation scenarios, recovery exercises, or targeted training tasks. Individual failures then become structured learning opportunities for the wider fleet.

Simulation provides a scalable environment for expanding the curriculum beyond situations that can be safely or economically generated with physical robots. Difficulty can be adjusted by changing terrain, object placement, sensor noise, communication quality, robot density, human activity, or task complexity. Rare and dangerous situations can be practiced repeatedly before the resulting capabilities are validated through controlled real-world deployment.

Real-world experience remains essential because simulation cannot reproduce every physical interaction or operational condition. Fleet observations reveal unexpected situations that designers did not include in the original curriculum. These experiences can be evaluated, clustered, prioritized, and converted into new training challenges. The curriculum therefore becomes a feedback loop between simulation, physical deployment, experience collection, learning, and validation.

Evaluation determines when the fleet is ready to progress. Advancement should not depend only on average reward or task success, because improvements in new capabilities can conceal degradation in older ones. Per-task performance, robustness, safety, recovery success, generalization, and retention should be evaluated across current and previous curriculum stages. Progression occurs when new competence is demonstrated without unacceptable loss of established knowledge.

Curriculum management also benefits from knowledge provenance and versioning. Each capability can retain information about the experiences, environments, robots, model versions, and curriculum stages that contributed to its development. When performance changes, this history helps identify which learning stage introduced the improvement or degradation. Models can then be compared, specialized, rolled back, or selectively retrained when necessary.

At fleet scale, the curriculum becomes a dynamic mechanism for directing collective learning resources. Robots generate experience in parallel, shared systems identify common weaknesses and emerging situations, training infrastructure creates appropriate learning challenges, and validated improvements return to compatible robots. The fleet therefore does not merely accumulate data; it actively decides what should be learned next and what knowledge must continue to be preserved.

Collective curriculum and continual learning ultimately transform robot deployment into an ongoing developmental process. Shared experience identifies what the fleet has encountered, replay preserves what it should remember, transfer learning spreads useful capabilities, and curriculum management determines the next frontier of learning. Combined with interference management and distributed updates, these mechanisms allow collective Physical AI to become progressively broader, more robust, and more capable without repeatedly forgetting previously acquired knowledge.

집단 커리큘럼 및 지속학습(Collective Curriculum and Continual Learning)은 플릿 지능(Fleet Intelligence)을 서로 독립된 학습 에피소드의 연속이 아니라 점진적으로 발전하는 학습 과정으로 구성한다. 집단 커리큘럼(Collective Curriculum)은 로봇이 어떤 작업, 환경, 실패, 협조 문제를 어떤 순서로 학습해야 하는지를 결정하며, 지속학습(Continual Learning)은 새로운 경험이 유입되는 동안 기존의 유용한 지식을 보존한다. 두 개념을 결합하면 로봇 플릿이 전체 운영 수명에 걸쳐 역량을 지속적으로 축적할 수 있다.

전통적인 로봇 학습은 고정된 데이터셋(Fixed Dataset)과 사전에 정의된 작업 분포(Task Distribution)를 따르는 경우가 많다. 그러나 실제 물리적 배포에서는 로봇이 새로운 레이아웃, 객체, 사용자, 팀원, 교란(Disturbance), 임무 요구사항을 지속적으로 경험한다. 따라서 학습 문제 자체가 시간에 따라 변화한다. 집단 커리큘럼은 플릿의 역량, 불확실성(Uncertainty), 운영 중요도, 새롭게 나타나는 역량 격차(Capability Gap)에 따라 경험과 학습 과제를 선택함으로써 이러한 변화하는 분포에 대응한다.

커리큘럼 학습(Curriculum Learning)은 이전에 획득한 역량이 더 어려운 행동을 학습하기 위한 기반이 되도록 복잡도를 점진적으로 증가시킨다. 로봇은 먼저 구조화된 공간에서 안정적인 내비게이션을 학습한 다음 동적 장애물 주변에서 동작하고, 팀원과 협조하며, 위치추정 실패(Localization Failure)에서 복구하고, 궁극적으로 복잡한 다중 로봇 임무를 수행할 수 있다. 이러한 진행 방식은 초기 학습 단계에서 불필요한 난이도를 줄이는 동시에 이후 단계에서 재사용할 수 있는 지식을 형성한다.

플릿 규모(Fleet Scale)에서는 하나의 사전 결정된 순서에 의존하는 대신 여러 로봇의 경험을 이용하여 커리큘럼을 생성할 수 있다. 여러 로봇이 유사한 상황에서 반복적으로 실패한다면 해당 상황의 학습 우선순위를 높일 수 있다. 반대로 플릿 전체에서 이미 안정적으로 수행되는 작업에는 상대적으로 적은 학습 자원을 할당할 수 있다. 따라서 커리큘럼은 개발과 배포 과정에서 고정된 상태로 유지되는 것이 아니라 집단 성능(Collective Performance)에 따라 지속적으로 변화한다.

유용한 집단 커리큘럼은 난이도(Difficulty), 새로움(Novelty), 관련성(Relevance)의 균형을 유지해야 한다. 지나치게 쉬운 경험은 학습 가치가 낮고, 현재 역량을 크게 넘어서는 과제는 불안정한 학습이나 의미 없는 실패를 발생시킬 수 있다. 기존 역량의 경계에 위치한 작업은 일반적으로 더 강한 학습 신호를 제공한다. 새로운 상황을 점진적으로 도입하면서 이미 숙달된 행동을 보존할 수 있도록 충분한 익숙한 경험도 함께 유지해야 한다.

서로 다른 로봇이 반드시 동일한 커리큘럼을 필요로 하는 것은 아니다. 이기종 체화(Heterogeneous Embodiment)는 서로 다른 센서, 이동 시스템, 매니퓰레이터(Manipulator), 연산 자원, 임무 역할을 가질 수 있다. 자율이동로봇(AMR)은 고급 내비게이션과 물류 커리큘럼을 필요로 할 수 있는 반면, 4족 보행 로봇(Quadruped)은 지형 통과와 안정성에 집중할 수 있다. 공유 작업 추상화(Shared Task Abstraction)는 이러한 전문화된 커리큘럼을 연결하면서 각 체화가 자신의 역량에 따라 발전하도록 할 수 있다.

집단 커리큘럼은 로봇 사이의 관계에 따라 난이도가 달라지는 협력 작업(Cooperative Task)도 포함할 수 있다. 초기 단계에서는 단순한 작업 할당(Task Allocation)이나 대형 유지(Formation Maintenance)를 학습하고, 이후 협력 탐색(Coordinated Exploration), 협력 운송(Cooperative Transport), 혼잡 관리(Congestion Management), 통신 제약 운영(Communication-Constrained Operation), 이기종 팀 임무(Heterogeneous Team Mission)로 발전할 수 있다. 점차 복잡해지는 상호작용 구조를 학습함으로써 단순한 협조 프리미티브(Coordination Primitive)에서 더욱 발전된 집단 행동을 형성할 수 있다.

지속학습(Continual Learning)은 전체 시스템을 처음부터 반복적으로 재학습하지 않고 이러한 연속적인 경험을 통합하는 메커니즘을 제공한다. 새로운 작업과 환경이 등장하면 모델은 중요한 기존 역량을 유지하면서 적응한다. 이를 위해서는 안정성-가소성 균형(Stability-Plasticity Balance)을 관리해야 한다. 시스템은 새로운 지식을 획득할 수 있을 만큼 충분한 가소성(Plasticity)을 유지하는 동시에 기존 기술에 대한 파괴적인 변화를 방지할 수 있을 만큼 충분한 안정성(Stability)을 유지해야 한다.

경험 재현(Experience Replay)은 이러한 균형을 유지하기 위한 중요한 메커니즘 가운데 하나이다. 새로운 커리큘럼 경험을 대표적인 과거 에피소드(Historical Episode)와 함께 학습함으로써 이전 역량을 활성 상태로 유지할 수 있다. 리플레이 버퍼(Replay Buffer)는 일상적인 운영, 희귀 실패(Rare Failure), 성공적인 복구, 안전 중요 사례(Safety-Critical Case), 이전 커리큘럼 단계의 대표 작업을 보존할 수 있다. 이를 통해 플릿은 새로운 역량으로 발전하면서도 중요한 기존 지식을 반복적으로 학습할 수 있다.

모듈형 및 파라미터 효율적 학습(Modular and Parameter-Efficient Learning)은 간섭(Interference)을 더욱 줄일 수 있다. 공유 인식(Shared Perception) 또는 월드 모델(World Model) 구성요소는 비교적 안정적으로 유지하면서 어댑터(Adapter), 정책 헤드(Policy Head), 기술 모듈(Skill Module) 또는 기타 특화 파라미터만 새로운 커리큘럼 단계에 맞추어 업데이트할 수 있다. 이를 통해 모든 파라미터를 동시에 변경하지 않고 새로운 역량을 추가할 수 있으며, 서로 다른 조건에서 운영되는 로봇별로 서로 다른 학습 경로를 지원할 수 있다.

커리큘럼 선택(Curriculum Selection)은 불확실성과 학습 진전도(Learning Progress)를 기준으로 결정할 수 있다. 모델이 높은 불확실성을 보이는 상황은 지식 격차(Knowledge Gap)를 나타낼 수 있으며, 빠른 성능 향상을 보이는 작업은 효과적인 학습 영역을 의미할 수 있다. 반대로 개선 없이 실패가 지속된다면 선행 기술(Prerequisite Skill)이 부족하다는 것을 나타낼 수 있다. 커리큘럼 관리자(Curriculum Manager)는 현재 역량과 목표 역량 사이의 격차를 연결하는 중간 작업을 선택하여 대응할 수 있다.

따라서 실패(Failure)는 단순히 바람직하지 않은 결과가 아니라 가치 있는 커리큘럼 신호(Curriculum Signal)가 된다. 위치추정 손실(Localization Loss), 내비게이션 교착상태(Navigation Deadlock), 파지 실패(Grasp Failure), 통신 장애(Communication Breakdown), 협조 오류(Coordination Error)는 플릿의 지식이 부족한 부분을 보여줄 수 있다. 이러한 사례를 탐지하고 검증하면 리플레이 에피소드, 시뮬레이션 시나리오, 복구 훈련 또는 표적 학습 작업(Targeted Training Task)으로 변환할 수 있다. 이를 통해 개별 실패가 전체 플릿을 위한 구조화된 학습 기회로 전환된다.

시뮬레이션(Simulation)은 실제 로봇으로 안전하거나 경제적으로 생성하기 어려운 상황까지 커리큘럼을 확장할 수 있는 확장 가능한 환경을 제공한다. 지형, 객체 배치, 센서 노이즈, 통신 품질, 로봇 밀도, 인간 활동, 작업 복잡도를 변화시켜 난이도를 조절할 수 있다. 희귀하고 위험한 상황을 반복적으로 연습한 뒤 생성된 역량을 통제된 실제 환경 배포(Controlled Real-World Deployment)를 통해 검증할 수 있다.

그러나 시뮬레이션이 모든 물리적 상호작용이나 운영 조건을 재현할 수 없기 때문에 실제 환경 경험(Real-World Experience)은 여전히 필수적이다. 플릿의 관측을 통해 설계자가 초기 커리큘럼에 포함하지 못했던 예상 밖의 상황을 발견할 수 있다. 이러한 경험을 평가하고, 군집화(Clustering)하고, 우선순위를 부여하여 새로운 학습 과제로 변환할 수 있다. 따라서 커리큘럼은 시뮬레이션, 물리적 배포, 경험 수집, 학습, 검증을 연결하는 피드백 루프(Feedback Loop)로 발전한다.

평가(Evaluation)는 플릿이 다음 단계로 발전할 준비가 되었는지를 결정한다. 새로운 역량의 향상이 기존 역량의 저하를 숨길 수 있기 때문에 평균 보상이나 작업 성공률만으로 다음 단계로 진행해서는 안 된다. 현재 및 이전 커리큘럼 단계에 걸쳐 작업별 성능, 강건성(Robustness), 안전, 복구 성공률, 일반화(Generalization), 지식 유지(Retention)를 평가해야 한다. 기존 지식의 허용할 수 없는 손실 없이 새로운 역량이 입증되었을 때 다음 단계로 진행할 수 있다.

커리큘럼 관리(Curriculum Management)는 지식 출처 추적(Knowledge Provenance)과 버전 관리(Versioning)를 통해 더욱 효과적으로 수행할 수 있다. 각각의 역량에는 해당 역량의 개발에 기여한 경험, 환경, 로봇, 모델 버전, 커리큘럼 단계에 관한 정보를 유지할 수 있다. 성능이 변화하면 이러한 이력을 이용하여 어떤 학습 단계에서 개선 또는 성능 저하가 발생했는지를 식별할 수 있다. 필요에 따라 모델을 비교하고, 전문화(Specialization)하고, 롤백(Rollback)하거나 선택적으로 재학습할 수 있다.

플릿 규모에서 커리큘럼은 집단 학습 자원(Collective Learning Resources)의 방향을 결정하는 동적 메커니즘이 된다. 로봇들은 병렬적으로 경험을 생성하고, 공유 시스템은 공통적인 약점과 새롭게 등장하는 상황을 식별하며, 학습 인프라는 이에 적절한 학습 과제를 생성하고, 검증된 개선 사항은 호환 가능한 로봇에 다시 전달된다. 따라서 플릿은 단순히 데이터를 축적하는 것이 아니라 다음에 무엇을 학습해야 하는지와 어떤 지식을 계속 보존해야 하는지를 능동적으로 결정한다.

궁극적으로 집단 커리큘럼 및 지속학습(Collective Curriculum and Continual Learning)은 로봇 배포를 지속적으로 발전하는 개발 과정(Ongoing Developmental Process)으로 변환한다. 공유 경험(Shared Experience)은 플릿이 무엇을 경험했는지를 식별하고, 경험 재현은 무엇을 기억해야 하는지를 보존하며, 전이학습(Transfer Learning)은 유용한 역량을 확산하고, 커리큘럼 관리는 다음 학습 영역(Next Frontier of Learning)을 결정한다. 간섭 관리(Interference Management) 및 분산 업데이트(Distributed Updates)와 결합하면 이러한 메커니즘은 집단 피지컬 AI(Collective Physical AI)가 기존에 획득한 지식을 반복적으로 망각하지 않으면서 점진적으로 더 광범위하고 강건하며 높은 역량을 갖추도록 한다.

##  

## 05.13. Fleet Data Flywheel

![](images/image15.png){width="7.268055555555556in" height="7.268055555555556in"}

A fleet data flywheel transforms routine robot operation into a continuous mechanism for improving collective intelligence. Every deployed robot generates observations, actions, outcomes, failures, interventions, and environmental interactions while performing useful work. Instead of treating these records as temporary logs, the fleet captures valuable experience and converts it into training resources that improve future models, policies, skills, and operational decisions.

The flywheel begins with deployment because real-world operation provides experiences that cannot be completely anticipated during offline development. Robots encounter changing layouts, unfamiliar objects, unusual traffic, sensor degradation, communication interruptions, human behavior, and unexpected task conditions. Each deployment therefore expands the distribution of situations represented in the fleet\'s accumulated knowledge and reveals gaps that existing models have not yet mastered.

Continuous collection does not mean that every sensor stream must be stored indefinitely. Large fleets can generate enormous quantities of camera, LiDAR, state, control, and diagnostic data, much of which may be repetitive. A practical data engine identifies useful episodes according to novelty, uncertainty, failure, intervention, task relevance, environmental diversity, and learning value. Selective capture concentrates storage and processing resources on experiences most likely to improve the system.

Metadata gives collected experience the context required for later reuse. Robot identity, embodiment, sensor configuration, software and model versions, task type, location category, operating conditions, timestamps, confidence, intervention history, and outcomes can accompany each episode. This information allows the learning system to distinguish universally useful experience from knowledge that applies only to particular robots, environments, or operational circumstances.

Data quality control is necessary before operational experience becomes training material. Sensor faults, synchronization errors, incorrect localization, corrupted logs, incomplete trajectories, or abnormal hardware conditions can create misleading examples. Automated validation can detect inconsistencies and assign confidence or quality scores, while uncertain or safety-critical cases can be routed for additional inspection. The objective is to prevent low-quality experience from silently contaminating collective models.

Failures and edge cases provide especially strong momentum to the flywheel. A navigation deadlock, localization loss, unexpected obstacle, failed grasp, task handoff error, communication breakdown, or human intervention identifies a boundary of current competence. These events can be extracted from routine fleet operation and converted into replay episodes, labeled examples, simulation scenarios, evaluation cases, or targeted curriculum tasks for subsequent learning.

Successful recoveries are equally valuable because they demonstrate how difficult situations can be resolved. When a robot encounters a failure and later completes the task through replanning, human guidance, another robot\'s assistance, or an alternative skill, the complete sequence provides richer information than the failure alone. The fleet can preserve these transitions and use them to train recovery policies that reduce future dependence on external intervention.

Human intervention can function as an important supervision channel within the data flywheel. Teleoperation, corrective commands, task reassignment, approval, rejection, and manual recovery reveal situations in which autonomous behavior was insufficient. These interactions can become demonstrations or preference signals for later learning. As models improve, intervention frequency can decline, while remaining interventions increasingly identify more difficult and informative edge cases.

Collected experience enters a data curation stage where redundant samples can be removed and valuable episodes prioritized. Clustering can identify recurring operational patterns, while novelty detection can expose previously unseen situations. Balanced datasets can preserve routine behavior together with failures, recoveries, rare environments, and safety-critical events. Curation therefore converts raw fleet history into a more compact and useful representation of operational knowledge.

The curated data can support several learning mechanisms simultaneously. Supervised learning can improve perception and prediction, reinforcement learning can refine policies, imitation learning can reproduce successful demonstrations, world models can learn environmental dynamics, and experience replay can preserve historical competence. The same operational episode may therefore contribute to multiple components of the Physical AI stack rather than serving only one training objective.

Simulation strengthens the flywheel by amplifying important real-world observations. A rare failure discovered by one robot can be reconstructed in simulation and varied across obstacle positions, sensor noise, terrain properties, payloads, robot configurations, or communication conditions. Thousands of related scenarios can then be generated from one physical event. Simulation converts sparse real-world evidence into broader training coverage without repeatedly exposing physical robots to dangerous conditions.

Training produces candidate improvements rather than automatically trusted models. Updated perception modules, world models, policies, skills, or adapters must be evaluated against current tasks and historical capabilities. Regression testing, replay evaluation, simulation, safety benchmarks, and controlled physical experiments determine whether new knowledge improves the fleet without introducing catastrophic interference or unacceptable degradation in previously reliable behaviors.

Validated models can be released through staged deployment rather than immediate fleet-wide replacement. Initial deployment to a small subset of robots provides evidence under real operating conditions. Performance, uncertainty, interventions, failures, and safety indicators can be monitored before the update expands to larger groups. Versioning and rollback mechanisms allow the system to recover if an apparently successful update produces unexpected behavior after deployment.

Once improved models return to operation, they alter the experiences generated by the fleet. Better navigation reduces some failures, stronger recovery creates new successful trajectories, improved perception exposes subtler edge cases, and new skills allow robots to enter more complex tasks. The data distribution therefore changes as intelligence improves. This creates the essential feedback mechanism of the flywheel: better models generate better and more informative future experience.

Fleet scale provides a compounding advantage because many robots can explore different portions of the operational distribution simultaneously. A situation encountered rarely by one robot may occur frequently somewhere across hundreds or thousands of deployed systems. Aggregating these distributed experiences increases the rate at which rare cases are discovered and validated. Deployment scale can therefore become a learning advantage rather than merely an operational expansion.

The flywheel can operate hierarchically across robot, site, on-premise, and broader fleet levels. Individual robots may perform local filtering and adaptation, while site infrastructure aggregates operational experience and identifies recurring patterns. Higher-level learning systems can combine knowledge across multiple deployments and redistribute validated improvements. This architecture reduces unnecessary data movement while preserving the benefits of large-scale collective learning.

Data governance, privacy, security, and provenance must remain integrated throughout the cycle. Operational data may contain sensitive environmental information, while corrupted or malicious contributions can damage shared intelligence. Access control, secure transfer, provenance tracking, retention policies, validation, and controlled model release help ensure that faster learning does not undermine trustworthiness. The flywheel must improve both capability and operational reliability.

The fleet data flywheel ultimately connects deployment, experience collection, curation, learning, validation, redistribution, and renewed deployment into one continuous loop. Shared experience supplies the data, replay preserves valuable history, transfer learning spreads knowledge, continual learning integrates new capabilities, and curriculum mechanisms determine what should be learned next. Each cycle transforms physical operation into reusable collective knowledge.

As the cycle repeats, the fleet becomes both the user and the producer of its own learning system. More operation generates broader experience, broader experience supports stronger models, stronger models enable more capable deployment, and expanded deployment generates still richer experience. The Fleet Data Flywheel therefore provides a scalable mechanism through which distributed Physical AI can progressively convert real-world activity into increasingly capable, adaptive, and robust collective intelligence.

플릿 데이터 플라이휠(Fleet Data Flywheel)은 일상적인 로봇 운영(Robot Operation)을 집단 지능(Collective Intelligence)을 지속적으로 향상시키는 메커니즘으로 전환한다. 배포된 모든 로봇은 실제 작업을 수행하면서 관측(Observation), 행동(Action), 결과(Outcome), 실패(Failure), 개입(Intervention), 환경과의 상호작용(Environmental Interaction)을 생성한다. 이러한 기록을 일시적인 로그로 취급하는 대신 플릿은 가치 있는 경험을 수집하고, 이를 미래의 모델, 정책(Policy), 기술(Skill), 운영 의사결정을 개선하는 학습 자원으로 변환한다.

플라이휠은 배포(Deployment)에서 시작된다. 실제 환경의 운영은 오프라인 개발 단계에서 완전히 예측할 수 없는 경험을 제공하기 때문이다. 로봇은 변화하는 레이아웃, 익숙하지 않은 객체, 비정상적인 교통 상황, 센서 성능 저하, 통신 중단, 인간 행동, 예상하지 못한 작업 조건을 경험한다. 따라서 각각의 배포는 플릿의 축적된 지식에 포함되는 상황 분포를 확장하고 기존 모델이 아직 충분히 학습하지 못한 지식 격차(Knowledge Gap)를 드러낸다.

지속적인 수집(Continuous Collection)이 모든 센서 스트림을 무기한 저장해야 한다는 것을 의미하지는 않는다. 대규모 플릿은 카메라, 라이다(LiDAR), 상태, 제어, 진단 데이터를 막대한 규모로 생성하며 그중 상당 부분은 반복적일 수 있다. 실용적인 데이터 엔진(Data Engine)은 새로움(Novelty), 불확실성(Uncertainty), 실패, 개입, 작업 관련성(Task Relevance), 환경 다양성, 학습 가치(Learning Value)를 기준으로 유용한 에피소드를 식별한다. 선택적 수집(Selective Capture)은 시스템 향상 가능성이 높은 경험에 저장 및 처리 자원을 집중시킨다.

메타데이터(Metadata)는 수집된 경험을 이후에 재사용하는 데 필요한 맥락(Context)을 제공한다. 로봇 식별정보, 체화(Embodiment), 센서 구성, 소프트웨어 및 모델 버전, 작업 유형, 위치 범주, 운영 조건, 타임스탬프(Timestamp), 신뢰도(Confidence), 개입 이력, 결과 등을 각 에피소드와 함께 저장할 수 있다. 이러한 정보는 학습 시스템이 보편적으로 유용한 경험과 특정 로봇, 환경 또는 운영 조건에서만 적용되는 지식을 구분하도록 한다.

운영 경험을 학습 자료로 활용하기 전에 데이터 품질 관리(Data Quality Control)가 필요하다. 센서 고장, 동기화 오류(Synchronization Error), 잘못된 위치추정(Localization), 손상된 로그, 불완전한 궤적(Trajectory), 비정상적인 하드웨어 상태는 잘못된 학습 사례를 생성할 수 있다. 자동 검증(Automated Validation)을 통해 불일치를 탐지하고 신뢰도 또는 품질 점수를 부여할 수 있으며, 불확실하거나 안전이 중요한 사례는 추가 검사를 위해 별도로 전달할 수 있다. 목표는 낮은 품질의 경험이 집단 모델을 조용히 오염시키는 것을 방지하는 것이다.

실패 및 엣지 케이스(Edge Case)는 플라이휠에 특히 강한 추진력을 제공한다. 내비게이션 교착상태(Navigation Deadlock), 위치추정 손실(Localization Loss), 예상하지 못한 장애물, 파지 실패(Grasp Failure), 작업 인계 오류(Task Handoff Error), 통신 장애(Communication Breakdown), 인간 개입은 현재 역량의 한계를 보여준다. 이러한 사건을 일상적인 플릿 운영에서 추출하여 경험 재현 에피소드(Replay Episode), 라벨링된 사례, 시뮬레이션 시나리오, 평가 사례 또는 이후 학습을 위한 표적 커리큘럼 작업(Targeted Curriculum Task)으로 변환할 수 있다.

성공적인 복구(Successful Recovery) 역시 어려운 상황을 해결하는 방법을 보여주기 때문에 매우 가치가 높다. 로봇이 실패를 경험한 이후 재계획(Replanning), 인간의 안내, 다른 로봇의 지원 또는 대체 기술(Alternative Skill)을 통해 작업을 완료하면 전체 과정은 실패 자체보다 더 풍부한 정보를 제공한다. 플릿은 이러한 전환 과정을 보존하여 향후 외부 개입에 대한 의존도를 줄이는 복구 정책(Recovery Policy)을 학습하는 데 활용할 수 있다.

인간 개입(Human Intervention)은 데이터 플라이휠 내부에서 중요한 지도 신호(Supervision Channel)로 기능할 수 있다. 원격조작(Teleoperation), 수정 명령(Corrective Command), 작업 재할당, 승인, 거부, 수동 복구는 자율 행동이 충분하지 않았던 상황을 보여준다. 이러한 상호작용은 이후 학습을 위한 시연(Demonstration) 또는 선호 신호(Preference Signal)가 될 수 있다. 모델이 개선될수록 개입 빈도는 감소하고, 남아 있는 개입 사례는 점차 더 어렵고 정보 가치가 높은 엣지 케이스를 나타낼 수 있다.

수집된 경험은 데이터 큐레이션(Data Curation) 단계로 들어가 중복 샘플을 제거하고 가치 있는 에피소드에 우선순위를 부여할 수 있다. 군집화(Clustering)는 반복되는 운영 패턴을 식별하고, 새로움 탐지(Novelty Detection)는 이전에 경험하지 못했던 상황을 발견할 수 있다. 균형 잡힌 데이터셋(Balanced Dataset)은 일상적인 행동과 함께 실패, 복구, 희귀 환경, 안전 중요 사건을 보존할 수 있다. 따라서 큐레이션은 원시 플릿 이력(Raw Fleet History)을 보다 압축되고 유용한 운영 지식의 표현으로 변환한다.

큐레이션된 데이터는 여러 학습 메커니즘을 동시에 지원할 수 있다. 지도학습(Supervised Learning)은 인식과 예측을 향상시키고, 강화학습(Reinforcement Learning)은 정책을 개선하며, 모방학습(Imitation Learning)은 성공적인 시연을 재현할 수 있다. 월드 모델(World Model)은 환경의 동역학을 학습하고, 경험 재현(Experience Replay)은 과거 역량을 보존한다. 따라서 하나의 운영 에피소드가 단일 학습 목적에만 사용되는 것이 아니라 피지컬 AI 스택(Physical AI Stack)의 여러 구성요소에 동시에 기여할 수 있다.

시뮬레이션(Simulation)은 중요한 실제 환경 관측을 증폭함으로써 플라이휠을 강화한다. 하나의 로봇에서 발견된 희귀 실패를 시뮬레이션에서 재구성한 후 장애물 위치, 센서 노이즈, 지형 특성, 적재량(Payload), 로봇 구성, 통신 조건 등을 변화시킬 수 있다. 하나의 실제 사건에서 수천 개의 관련 시나리오를 생성할 수 있다. 이를 통해 시뮬레이션은 물리적 로봇을 위험한 조건에 반복적으로 노출시키지 않으면서 희소한 실제 증거를 광범위한 학습 범위로 확장한다.

학습(Training)은 자동으로 신뢰할 수 있는 모델이 아니라 후보 개선 사항(Candidate Improvement)을 생성한다. 업데이트된 인식 모듈, 월드 모델, 정책, 기술 또는 어댑터(Adapter)는 현재 작업과 과거 역량을 기준으로 평가해야 한다. 회귀 시험(Regression Testing), 리플레이 평가(Replay Evaluation), 시뮬레이션, 안전 벤치마크(Safety Benchmark), 통제된 물리적 실험을 통해 새로운 지식이 치명적 간섭(Catastrophic Interference)이나 기존의 신뢰할 수 있는 행동에 허용할 수 없는 성능 저하를 발생시키지 않으면서 플릿을 개선하는지를 판단한다.

검증된 모델(Validated Model)은 즉시 전체 플릿을 교체하는 대신 단계적 배포(Staged Deployment)를 통해 출시할 수 있다. 초기에는 소수의 로봇에 배포하여 실제 운영 조건에서 성능 증거를 확보한다. 업데이트를 더 큰 로봇 그룹으로 확장하기 전에 성능, 불확실성, 개입, 실패, 안전 지표를 모니터링할 수 있다. 버전 관리(Versioning)와 롤백(Rollback) 메커니즘은 성공적으로 보였던 업데이트가 실제 배포 이후 예상하지 못한 행동을 발생시키는 경우 시스템을 이전 상태로 복구할 수 있도록 한다.

개선된 모델이 다시 운영 환경으로 돌아가면 플릿에서 생성되는 경험 자체가 변화한다. 향상된 내비게이션은 일부 실패를 감소시키고, 더 강력한 복구 능력은 새로운 성공 궤적을 생성하며, 개선된 인식은 더욱 미묘한 엣지 케이스를 발견하고, 새로운 기술은 로봇이 더 복잡한 작업을 수행할 수 있도록 한다. 따라서 지능이 향상됨에 따라 데이터 분포(Data Distribution)도 변화한다. 더 나은 모델이 더 우수하고 정보 가치가 높은 미래 경험을 생성하는 것이 플라이휠의 핵심 피드백 메커니즘(Feedback Mechanism)이다.

플릿 규모(Fleet Scale)는 많은 로봇이 운영 분포의 서로 다른 영역을 동시에 탐색할 수 있기 때문에 복리 효과(Compounding Advantage)를 제공한다. 하나의 로봇에서는 드물게 발생하는 상황이 수백 또는 수천 대의 배포 시스템 전체에서는 빈번하게 발생할 수 있다. 이러한 분산 경험(Distributed Experience)을 통합하면 희귀 사례를 발견하고 검증하는 속도가 증가한다. 따라서 배포 규모는 단순한 운영 확장이 아니라 학습상의 이점(Learning Advantage)으로 발전할 수 있다.

플라이휠은 로봇, 사이트(Site), 온프레미스(On-Premise), 더 광범위한 플릿 수준에 걸쳐 계층적으로 운영할 수 있다. 개별 로봇은 로컬 필터링(Local Filtering)과 적응을 수행하고, 사이트 인프라는 운영 경험을 통합하여 반복되는 패턴을 식별할 수 있다. 상위 수준 학습 시스템은 여러 배포 환경의 지식을 결합하고 검증된 개선 사항을 다시 배포할 수 있다. 이러한 아키텍처는 불필요한 데이터 이동을 줄이면서 대규모 집단 학습(Large-Scale Collective Learning)의 장점을 유지한다.

데이터 거버넌스(Data Governance), 프라이버시(Privacy), 보안(Security), 출처 추적(Provenance)은 전체 사이클에 통합되어야 한다. 운영 데이터에는 민감한 환경 정보가 포함될 수 있으며, 손상되거나 악의적인 데이터가 공유 지능을 저하시킬 수도 있다. 접근 제어(Access Control), 보안 전송(Secure Transfer), 출처 추적, 보존 정책(Retention Policy), 검증, 통제된 모델 배포를 통해 빠른 학습이 시스템의 신뢰성을 훼손하지 않도록 해야 한다. 플라이휠은 역량뿐 아니라 운영 신뢰성(Operational Reliability)도 함께 향상시켜야 한다.

궁극적으로 플릿 데이터 플라이휠(Fleet Data Flywheel)은 배포, 경험 수집(Experience Collection), 큐레이션, 학습, 검증, 재배포(Redistribution), 그리고 새로운 배포를 하나의 지속적인 순환 구조로 연결한다. 공유 경험(Shared Experience)은 데이터를 제공하고, 경험 재현은 가치 있는 과거 이력을 보존하며, 전이학습(Transfer Learning)은 지식을 확산하고, 지속학습(Continual Learning)은 새로운 역량을 통합하며, 커리큘럼 메커니즘(Curriculum Mechanism)은 다음에 무엇을 학습해야 하는지를 결정한다. 각각의 사이클은 실제 물리적 운영을 재사용 가능한 집단 지식(Collective Knowledge)으로 변환한다.

이러한 사이클이 반복되면서 플릿은 자체 학습 시스템의 사용자이자 생산자가 된다. 더 많은 운영은 더욱 폭넓은 경험을 생성하고, 더 폭넓은 경험은 더 강력한 모델을 지원하며, 더 강력한 모델은 더욱 높은 수준의 배포를 가능하게 하고, 확장된 배포는 다시 더욱 풍부한 경험을 생성한다. 따라서 플릿 데이터 플라이휠은 분산 피지컬 AI(Distributed Physical AI)가 실제 세계의 활동을 점진적으로 더욱 높은 역량, 적응성(Adaptability), 강건성(Robustness)을 갖춘 집단 지능으로 전환할 수 있도록 하는 확장 가능한 메커니즘을 제공한다.

##  

## 05.14. Collective Learning Pipeline [w/Code]

![](images/image16.png){width="7.268055555555556in" height="7.268055555555556in"}

A collective learning pipeline provides the operational structure through which experiences generated by many robots are transformed into shared and reusable intelligence. It connects physical deployment, data collection, experience management, distributed learning, validation, knowledge integration, and model redistribution into a continuous system. Rather than treating learning as an isolated offline activity, the pipeline embeds learning directly into the lifecycle of a robot fleet.

The pipeline begins at the robot level, where individual agents perform missions and interact with the physical world. Each robot continuously produces observations, actions, state transitions, task outcomes, rewards, failures, recovery attempts, communication events, and human interventions. These experiences represent the raw material of collective learning because they capture situations encountered under actual operating conditions across different robots, environments, and tasks.

Local processing determines which experiences should leave the robot and enter the wider learning system. Raw sensor streams may be too large, repetitive, sensitive, or irrelevant to transmit continuously. Robots can therefore detect novelty, uncertainty, failures, interventions, unusual state transitions, or important task outcomes and package selected episodes with metadata. This creates a filtered experience stream with substantially higher learning value than indiscriminate data collection.

Metadata provides the context required to interpret distributed robot experience correctly. Each episode can identify the robot embodiment, sensor configuration, model and software versions, task, environment, timestamp, operating conditions, confidence, and outcome. Without this information, experiences collected by heterogeneous robots can be incorrectly combined. Context allows later stages to determine compatibility, relevance, freshness, and transferability before knowledge is reused.

Selected experiences can enter local, site-level, or fleet-level memory depending on communication and deployment architecture. Local replay buffers preserve recent robot-specific experience, while on-premise systems can aggregate knowledge from robots operating within the same facility. Higher-level repositories may combine selected experience across multiple sites. This hierarchical memory structure reduces unnecessary data movement while creating progressively broader collective knowledge.

Data curation transforms distributed experience into structured learning resources. Duplicate or low-quality samples can be removed, while rare failures, successful recoveries, novel environments, difficult interactions, and safety-critical episodes receive greater attention. Clustering, prioritization, balancing, provenance tracking, and quality scoring help construct datasets that represent both normal operation and important edge cases rather than simply reflecting the most frequently generated data.

The curated experience can feed several learning mechanisms according to the capability being improved. Supervised learning can refine perception, imitation learning can reproduce successful behavior, reinforcement learning can optimize policies, and world models can learn temporal dynamics and future consequences. Multi-agent learning can use joint trajectories to improve coordination, while replay mechanisms preserve historical knowledge during adaptation to new experiences.

Distributed learning allows computational work to occur at different levels of the architecture. Robots with sufficient resources may perform lightweight local adaptation, while on-premise infrastructure can conduct more substantial training using site-level experience. Broader fleet infrastructure can integrate knowledge across deployments. Federated learning, distributed model updates, parameter-efficient adaptation, and hierarchical aggregation provide different mechanisms for combining these learning contributions.

Not every locally learned improvement should become global fleet knowledge. Candidate updates must first be evaluated for compatibility and usefulness. A policy adapted to one robot, terrain, payload, or sensor configuration may not transfer safely to another platform. The pipeline therefore compares embodiment, task, environment, model version, performance evidence, and operational context before determining whether knowledge should remain local, become site-specific, or propagate more broadly.

Knowledge conflict management becomes necessary when different robots produce incompatible learning signals. One experience may favor cautious behavior while another favors aggressive execution because their operating conditions differ. Rather than averaging every update into one universal model, the pipeline can detect conflicts and preserve specialized policies, adapters, skills, or model branches. Context-aware routing can then activate the appropriate knowledge for each operating situation.

Continual learning mechanisms protect established capabilities while new knowledge enters the system. Historical replay, parameter protection, modular learning, adapters, and balanced sampling reduce catastrophic interference. The objective is not simply to maximize performance on the newest fleet data, but to expand capability while preserving navigation, manipulation, coordination, recovery, and safety behaviors that have already been validated during previous learning stages.

A collective curriculum determines which knowledge gaps deserve learning resources next. Repeated failures, high uncertainty, frequent human intervention, emerging environments, or insufficient coordination performance can become targeted training objectives. Tasks can be ordered according to difficulty and prerequisite capabilities. The learning pipeline therefore does more than process incoming data; it actively converts fleet weaknesses into structured challenges that guide future capability development.

Simulation can amplify important experiences before new models return to physical robots. Rare events collected during deployment can be reconstructed and systematically varied across terrain, sensor noise, robot density, payload, communication quality, or environmental conditions. Simulation provides large-scale training and stress testing while reducing physical risk. Real-world episodes keep these synthetic variations grounded in operationally relevant problems.

Evaluation and validation form a critical gate between learning and deployment. Candidate models should be tested against new objectives as well as previously mastered capabilities. Task success, robustness, generalization, recovery performance, safety, knowledge retention, and cross-robot compatibility can be evaluated using replay datasets, simulation, digital twins, benchmarks, and controlled physical experiments. Improvements that introduce unacceptable regression should not proceed automatically.

Validated knowledge can then be packaged according to its appropriate scope. Some updates may modify a common perception or world-model backbone, while others become policy heads, low-rank adapters, robot-specific controllers, reusable skills, or environment-specific modules. Version information, provenance, compatibility requirements, dependencies, and validation evidence accompany these packages so receiving robots can determine how and where they should be applied.

Deployment should proceed gradually rather than replacing the entire fleet simultaneously. A candidate model or skill can first be released to a small group of compatible robots and monitored under real operating conditions. If performance remains stable, distribution can expand to a site and eventually to the wider fleet. Monitoring, version management, rollback, and safety supervision provide protection when unexpected behavior appears after release.

Once updated robots return to operation, they generate a new distribution of experience. Previously common failures may decline, new capabilities may expose more difficult situations, and improved policies may create new forms of coordination and recovery behavior. These experiences re-enter the pipeline and become material for the next learning cycle. Deployment is therefore both the output of collective learning and the source of its next generation of data.

The complete pipeline forms a closed loop from physical experience to collective knowledge and back to physical execution. Robots experience the world, useful episodes are selected and curated, distributed learning produces candidate improvements, conflicts and interference are managed, models are validated, and appropriate knowledge is redistributed. Each cycle converts dispersed individual experience into increasingly reusable fleet-level intelligence.

At scale, the collective learning pipeline becomes the learning backbone of Collective Physical AI. Shared experience supplies evidence, federated and distributed learning combine contributions, replay preserves memory, transfer learning spreads capabilities, curriculum learning directs progress, and the fleet data flywheel sustains continuous improvement. The result is a robot fleet that does not merely operate as many individual machines, but progressively learns as a connected collective system.

집단 학습 파이프라인(Collective Learning Pipeline)은 여러 로봇이 생성한 경험을 공유되고 재사용 가능한 지능(Shared and Reusable Intelligence)으로 변환하는 운영 구조를 제공한다. 이는 물리적 배포(Physical Deployment), 데이터 수집(Data Collection), 경험 관리(Experience Management), 분산 학습(Distributed Learning), 검증(Validation), 지식 통합(Knowledge Integration), 모델 재배포(Model Redistribution)를 하나의 지속적인 시스템으로 연결한다. 학습을 독립적인 오프라인 활동으로 취급하는 대신 로봇 플릿(Robot Fleet)의 전체 생명주기에 직접 통합한다.

파이프라인은 개별 에이전트가 임무를 수행하고 물리적 세계와 상호작용하는 로봇 수준(Robot Level)에서 시작된다. 각 로봇은 관측(Observation), 행동(Action), 상태 전이(State Transition), 작업 결과(Task Outcome), 보상(Reward), 실패(Failure), 복구 시도(Recovery Attempt), 통신 이벤트(Communication Event), 인간 개입(Human Intervention)을 지속적으로 생성한다. 이러한 경험은 서로 다른 로봇, 환경, 작업의 실제 운영 조건에서 발생하는 상황을 담고 있기 때문에 집단 학습(Collective Learning)의 원재료가 된다.

로컬 처리(Local Processing)는 어떤 경험이 로봇을 벗어나 더 넓은 학습 시스템으로 전달되어야 하는지를 결정한다. 원시 센서 스트림(Raw Sensor Stream)은 지속적으로 전송하기에는 지나치게 크거나 반복적이고 민감하거나 학습 가치가 낮을 수 있다. 따라서 로봇은 새로움(Novelty), 불확실성(Uncertainty), 실패, 개입, 비정상적인 상태 전이 또는 중요한 작업 결과를 탐지하고 선택된 에피소드를 메타데이터(Metadata)와 함께 패키지화할 수 있다. 이를 통해 무차별적인 데이터 수집보다 훨씬 높은 학습 가치를 가진 필터링된 경험 스트림(Filtered Experience Stream)을 생성한다.

메타데이터는 분산된 로봇 경험을 올바르게 해석하는 데 필요한 맥락(Context)을 제공한다. 각 에피소드에는 로봇 체화(Embodiment), 센서 구성, 모델 및 소프트웨어 버전, 작업, 환경, 타임스탬프(Timestamp), 운영 조건, 신뢰도(Confidence), 결과를 기록할 수 있다. 이러한 정보가 없으면 이기종 로봇(Heterogeneous Robots)에서 수집된 경험이 잘못 결합될 수 있다. 맥락 정보는 이후 단계에서 지식을 재사용하기 전에 호환성(Compatibility), 관련성(Relevance), 최신성(Freshness), 전이 가능성(Transferability)을 판단할 수 있도록 한다.

선택된 경험은 통신 및 배포 아키텍처에 따라 로컬, 사이트 수준(Site-Level), 플릿 수준(Fleet-Level)의 메모리로 전달될 수 있다. 로컬 리플레이 버퍼(Local Replay Buffer)는 최근의 로봇 특화 경험을 보존하고, 온프레미스 시스템(On-Premise System)은 동일한 시설에서 운영되는 로봇들의 지식을 통합할 수 있다. 상위 수준 저장소는 여러 사이트에서 선택된 경험을 결합할 수 있다. 이러한 계층적 메모리 구조(Hierarchical Memory Structure)는 불필요한 데이터 이동을 줄이면서 점차 더 광범위한 집단 지식을 형성한다.

데이터 큐레이션(Data Curation)은 분산 경험을 구조화된 학습 자원으로 변환한다. 중복되거나 품질이 낮은 샘플은 제거하고, 희귀 실패(Rare Failure), 성공적인 복구, 새로운 환경, 어려운 상호작용, 안전 중요 에피소드(Safety-Critical Episode)에 더 높은 우선순위를 부여할 수 있다. 군집화(Clustering), 우선순위화(Prioritization), 균형화(Balancing), 출처 추적(Provenance Tracking), 품질 평가(Quality Scoring)를 통해 단순히 가장 빈번하게 생성되는 데이터가 아니라 정상 운영과 중요한 엣지 케이스(Edge Case)를 모두 표현하는 데이터셋을 구성할 수 있다.

큐레이션된 경험은 개선하려는 역량에 따라 여러 학습 메커니즘으로 전달될 수 있다. 지도학습(Supervised Learning)은 인식을 개선하고, 모방학습(Imitation Learning)은 성공적인 행동을 재현하며, 강화학습(Reinforcement Learning)은 정책(Policy)을 최적화할 수 있다. 월드 모델(World Model)은 시간적 동역학과 미래 결과를 학습할 수 있다. 다중 에이전트 학습(Multi-Agent Learning)은 공동 궤적(Joint Trajectory)을 활용하여 협조를 개선하고, 경험 재현(Experience Replay)은 새로운 경험에 적응하는 과정에서 과거 지식을 보존한다.

분산 학습은 아키텍처의 서로 다른 수준에서 연산 작업을 수행할 수 있도록 한다. 충분한 자원을 가진 로봇은 경량 로컬 적응(Lightweight Local Adaptation)을 수행하고, 온프레미스 인프라(On-Premise Infrastructure)는 사이트 수준 경험을 이용하여 더 큰 규모의 학습을 수행할 수 있다. 더 광범위한 플릿 인프라는 여러 배포 환경의 지식을 통합할 수 있다. 연합학습(Federated Learning), 분산 모델 업데이트(Distributed Model Updates), 파라미터 효율적 적응(Parameter-Efficient Adaptation), 계층적 통합(Hierarchical Aggregation)은 이러한 학습 기여를 결합하기 위한 서로 다른 메커니즘을 제공한다.

로컬에서 학습된 모든 개선 사항이 전역 플릿 지식(Global Fleet Knowledge)이 되어야 하는 것은 아니다. 후보 업데이트(Candidate Update)는 먼저 호환성과 유용성을 평가해야 한다. 특정 로봇, 지형, 적재량(Payload), 센서 구성에 적응된 정책이 다른 플랫폼으로 안전하게 전이되지 않을 수 있다. 따라서 파이프라인은 지식을 로컬에 유지할지, 사이트 특화 지식(Site-Specific Knowledge)으로 사용할지, 더 광범위하게 확산할지를 결정하기 전에 체화, 작업, 환경, 모델 버전, 성능 증거(Performance Evidence), 운영 맥락을 비교한다.

서로 다른 로봇이 호환되지 않는 학습 신호를 생성하면 지식 충돌 관리(Knowledge Conflict Management)가 필요하다. 운영 조건이 다르기 때문에 하나의 경험은 신중한 행동을 선호하고 다른 경험은 적극적인 실행을 선호할 수 있다. 모든 업데이트를 하나의 범용 모델로 평균화하는 대신 파이프라인은 충돌을 탐지하고 전문화된 정책(Specialized Policy), 어댑터(Adapter), 기술(Skill), 모델 분기(Model Branch)를 유지할 수 있다. 이후 상황 인식 라우팅(Context-Aware Routing)을 통해 각각의 운영 상황에 적절한 지식을 활성화할 수 있다.

지속학습(Continual Learning) 메커니즘은 새로운 지식이 시스템으로 유입되는 동안 기존 역량을 보호한다. 과거 경험 재현(Historical Replay), 파라미터 보호(Parameter Protection), 모듈형 학습(Modular Learning), 어댑터, 균형 샘플링(Balanced Sampling)은 치명적 간섭(Catastrophic Interference)을 감소시킨다. 목표는 단순히 가장 최신 플릿 데이터에서 성능을 최대화하는 것이 아니라 이전 학습 단계에서 이미 검증된 내비게이션, 조작(Manipulation), 협조(Coordination), 복구, 안전 행동을 유지하면서 새로운 역량을 확장하는 것이다.

집단 커리큘럼(Collective Curriculum)은 다음에 어떤 지식 격차에 학습 자원을 투입해야 하는지를 결정한다. 반복되는 실패, 높은 불확실성, 빈번한 인간 개입, 새롭게 등장하는 환경 또는 부족한 협조 성능을 표적 학습 목표(Targeted Training Objective)로 변환할 수 있다. 작업은 난이도와 선행 역량(Prerequisite Capability)에 따라 순서화할 수 있다. 따라서 학습 파이프라인은 단순히 유입되는 데이터를 처리하는 것을 넘어 플릿의 약점을 미래의 역량 개발을 안내하는 구조화된 학습 과제로 능동적으로 변환한다.

시뮬레이션(Simulation)은 새로운 모델이 실제 로봇으로 돌아가기 전에 중요한 경험을 증폭할 수 있다. 실제 배포에서 수집된 희귀 사건을 재구성하고 지형, 센서 노이즈, 로봇 밀도, 적재량, 통신 품질 또는 환경 조건을 체계적으로 변화시킬 수 있다. 시뮬레이션은 물리적 위험을 줄이면서 대규모 학습과 스트레스 테스트(Stress Testing)를 제공한다. 실제 환경 에피소드(Real-World Episode)는 이러한 합성 변형이 운영상 중요한 문제에 기반하도록 한다.

평가 및 검증(Evaluation and Validation)은 학습과 배포 사이의 핵심 게이트(Gate)를 형성한다. 후보 모델은 새로운 목표뿐 아니라 이전에 숙달된 역량에 대해서도 시험되어야 한다. 작업 성공률, 강건성(Robustness), 일반화(Generalization), 복구 성능, 안전, 지식 유지(Knowledge Retention), 로봇 간 호환성을 리플레이 데이터셋, 시뮬레이션, 디지털 트윈(Digital Twin), 벤치마크(Benchmark), 통제된 물리적 실험을 이용하여 평가할 수 있다. 허용할 수 없는 성능 퇴행(Regression)을 발생시키는 개선 사항은 자동으로 다음 단계로 진행되어서는 안 된다.

검증된 지식은 적절한 적용 범위에 따라 패키지화할 수 있다. 일부 업데이트는 공통 인식(Common Perception) 또는 월드 모델 백본(World-Model Backbone)을 변경할 수 있으며, 다른 업데이트는 정책 헤드(Policy Head), 저랭크 어댑터(Low-Rank Adapter), 로봇 특화 제어기(Robot-Specific Controller), 재사용 가능한 기술(Reusable Skill), 환경 특화 모듈(Environment-Specific Module)이 될 수 있다. 버전 정보, 출처, 호환성 요구사항, 의존성(Dependency), 검증 증거가 이러한 패키지에 함께 포함되어 수신 로봇이 어디에 어떻게 적용할지를 판단할 수 있도록 한다.

배포(Deployment)는 전체 플릿을 동시에 교체하는 방식이 아니라 점진적으로 진행되어야 한다. 후보 모델 또는 기술을 먼저 소수의 호환 가능한 로봇에 배포하여 실제 운영 조건에서 모니터링할 수 있다. 성능이 안정적으로 유지되면 사이트 전체로 확장하고 궁극적으로 더 넓은 플릿으로 배포할 수 있다. 모니터링(Monitoring), 버전 관리(Version Management), 롤백(Rollback), 안전 감독(Safety Supervision)은 출시 이후 예상하지 못한 행동이 발생하는 경우 시스템을 보호한다.

업데이트된 로봇이 다시 운영에 투입되면 새로운 경험 분포(Experience Distribution)가 생성된다. 이전에 빈번했던 실패는 감소할 수 있고, 새로운 역량은 더욱 어려운 상황을 드러낼 수 있으며, 향상된 정책은 새로운 형태의 협조 및 복구 행동을 생성할 수 있다. 이러한 경험은 다시 파이프라인으로 유입되어 다음 학습 사이클의 재료가 된다. 따라서 배포는 집단 학습의 출력(Output)이면서 동시에 다음 세대 데이터의 원천(Source)이 된다.

전체 파이프라인은 물리적 경험(Physical Experience)에서 집단 지식으로, 그리고 다시 물리적 실행(Physical Execution)으로 이어지는 폐쇄 루프(Closed Loop)를 형성한다. 로봇은 세계를 경험하고, 유용한 에피소드는 선택되고 큐레이션되며, 분산 학습을 통해 후보 개선 사항이 생성된다. 이후 충돌과 간섭을 관리하고 모델을 검증한 다음 적절한 지식을 다시 배포한다. 각각의 사이클은 분산되어 있던 개별 경험을 점점 더 재사용 가능한 플릿 수준 지능(Fleet-Level Intelligence)으로 변환한다.

대규모 환경에서 집단 학습 파이프라인은 집단 피지컬 AI(Collective Physical AI)의 학습 백본(Learning Backbone)이 된다. 공유 경험(Shared Experience)은 증거를 제공하고, 연합 및 분산 학습(Federated and Distributed Learning)은 여러 로봇의 기여를 통합하며, 경험 재현은 기억을 보존하고, 전이학습(Transfer Learning)은 역량을 확산하며, 커리큘럼 학습(Curriculum Learning)은 발전 방향을 결정하고, 플릿 데이터 플라이휠(Fleet Data Flywheel)은 지속적인 개선을 유지한다. 그 결과 로봇 플릿은 단순히 다수의 개별 기계로 운영되는 것을 넘어 서로 연결된 하나의 집단 시스템(Collective System)으로서 지속적으로 학습하고 발전하게 된다.
