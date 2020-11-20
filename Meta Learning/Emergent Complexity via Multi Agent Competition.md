
# Abstract
Reinforcement learning algorithms can train agents that solve problems in com-plex, interesting environments. Normally, the complexity of the trained agent isclosely related to the complexity of the environment. This suggests that a highlycapable agent requires a complex environment for training. In this paper, we pointout that a competitive multi-agent environment trained with self-play can producebehaviors that are far more complex than the environment itself. We also point outthat such environments come with a natural curriculum, because for any skill level,an environment full of agents of this level will have the right level of difficulty.This work introduces several competitive multi-agent environments where agentscompete in a 3D world with simulated physics. The trained agents learn awide variety of complex and interesting skills, even though the environmentthemselves are relatively simple. The skills include behaviors such as running,blocking, ducking, tackling, fooling opponents, kicking, and defending usingboth arms and legs. A highlight of the learned behaviors can be found here:https://goo.gl/eR7fbX.

강화 학습 알고리즘은 복잡하고 흥미로운 환경에서 문제를 해결하는 요원을 훈련시킬 수 있다. 일반적으로 훈련된 에이전트의 복잡성은 환경의 복잡성과 밀접한 관련이 있다. 이는 성능이 뛰어난 에이전트가 훈련을 위해 복잡한 환경을 필요로 한다는 것을 시사한다. 본 논문에서는, 자기 놀이로 훈련된 경쟁적인 멀티 에이전트 환경이 환경 자체보다 훨씬 더 복잡한 행동 양식을 만들어 낼 수 있다는 점을 지적한다. 우리는 또한 그러한 환경은 자연적인 커리큘럼과 함께 온다는 것을 지적한다. 왜냐하면 어떤 기술 수준이든, 이 수준의 요원으로 가득 찬 환경은 적절한 수준의 난이도를 가질 것이기 때문이다.이 연구는 에이전트들이 3D 세계에서 모의 물리학으로 경쟁하는 몇 가지 경쟁적인 멀티 에이전트 환경을 소개한다. 훈련된 요원들은 환경 자체가 비교적 단순하지만, 다양하고 복잡하고 흥미로운 기술을 배운다. 기술에는 달리기, 블로킹, 오리치기, 태클하기, 상대를 속이기, 발로 차고, 팔과 다리를 모두 사용하여 방어하는 등의 행동이 포함된다. 학습된 행동의 하이라이트는 여기서 찾을 수 있다:https://goo.gl/eR7fbX.


# Intro
강화학습(RL)은 우수한 강화학습 알고리즘이 존재하기 때문에 흥미롭다(Mnih et al., 2015; Silver et al., 2016; Schulman et al., 2015; Lilicrap et al., 2015; Schulman et al., 2017). 아타리 게임을 픽셀(Mnih et al.,2015)에서 플레이할 에이전트를 훈련시키거나 휴머노이드(Humanoid)를 걸어보도록 할 수 있다(Schulman et al., 2017). RL은 부분적으로 RL 알고리즘이 환경의 적절한 커리큘럼에서 훈련될 때 광범위하게 유능한 에이전트를 생성하는 것을 상상하기 쉽기 때문에 흥미진진하다.


일반적으로 고도로 복잡한 작업을 수행하도록 에이전트를 교육하려면 고도로 복잡한 환경이 필요하며, 이러한 환경은 생성하기 어려울 수 있다. 그러나, 에이전트들에 의해 생성된 행동이 환경보다 훨씬 더 복잡할 수 있는 환경의 종류가 있다; 이것은 자기 놀이로 훈련된 경쟁적인 멀티 에이전트 환경의 공통점이다. 그러한 환경은 매우 매력적인 두 가지 특성을 가지고 있다. (1) 매우 단순한 경쟁적 다중 에이전트 환경도 극도로 복잡한 행동을 일으킬 수 있다. 예를 들어 바둑은 규칙이 매우 간단하지만, 이기기 위해 필요한 전략은 매우 복잡하다. 이러한 환경의 복잡성은 그 환경에서 작용하는 경쟁 대리점에 의해 주도되기 때문이다. 따라서 다른 에이전트들이 유능해질수록 환경은 사실상 복잡해진다. (2) 자기 놀이로 훈련할 때 경쟁적인 멀티 에이전트 환경은 에이전트들에게 완벽한 커리큘럼을 제공한다. 이는 에이전트가 얼마나 약하거나 강한지 명명자가 다른 비교가능성의 에이전트들로 채워진 환경이 에이전트에게 올바른 도전을 제공하기 때문에 발생하며, 이는 최대 속도의 학습을 용이하게 하고 막히는 것을 피한다.


경쟁적인 멀티에이전트 환경에서 자기 플레이는 새로운 아이디어가 아니다. TD-gammon(Tesauro, 1995)에서 이미 탐구되었고 알파고(Silver et al., 2016)와 도타 2(OpenAI)에서 정제되었다.두 경우 모두 결과적인 행동이 환경 자체보다 훨씬 더 복잡했고, 이들 놀이 접근방식은 요원들에게 각 과제에 대해 완벽하게 조정된 커리큘럼을 제공했다. 본 논문에서는 경쟁력 있는 멀티에이전트 환경에 대한 아이디어가 결실을 맺을 수 있는지 조사한다. ∗오픈에서 인턴으로 하는 작업AI. tbansal@cs.umass.edu 다른 도메인과의 통신: 특히, 균형, 손재주 및 조작이 핵심 기술인 지속적인 제어 영역에서.

좀 더 자세히 설명하면, 경쟁 환경에서 성공하기 위해 에이전트가 고도로 발달한 운동 기술을 배워야 하는 MuJoCo 프레임워크(Todorov et al., 2012)를 사용하여 시뮬레이트 물리학을 가진 3D 세계에서 경쟁 목표를 가진 여러 멀티 에이전트 작업을 소개한다. 최근 정책 구배 알고리즘인 근위부 정책 최적화(Schulman et al., 2017)의 분산 구현을 사용하여 에이전트를 교육한다. 환경 탐사를 돕기 위해 간단한 탐색 커리큘럼을 추가함으로써 우리는 에이전트들이 그들의 목표를 달성하기 위해 높은 수준의 민첩성을 배운다는 것을 발견한다. 특히 우리는 보상을 고안하는 것이 어려울 수 있는 수많은 새로운 기술들을 발견한다. 구체적으로 에이전트들은 달리기, 블로킹, 오리치기, 태클하기, 상대를 속이기, 팔과 다리를 이용한 발차기, 방어 등 다양한 기술과 행동을 배웠다. 다양한 작업에 대해 학습된 행동의 하이라이트는 https://goo.gl/eR7fbX에서 확인할 수 있다.

## 참고자료
https://www.slideshare.net/WoongwonLee/trpo-87165690
https://reinforcement-learning-kr.github.io/2018/06/24/5_trpo/