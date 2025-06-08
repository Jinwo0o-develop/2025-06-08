# 2025-06-08 (게임캐릭터 피격 및 공격구현)

# 함수 설명
__init__ 함수에서 게임 캐릭터를 받음<br>
is_alive 함수는 게임 캐릭터 생사여부 확인<br>
get_attacked함수에서 공격한 캐릭터의 공격력만큼 체력을 깍음<br>
attack함수 게임 캐릭터가 살아 있으면 다른 캐릭터 공격<br>
__str__함수 출력을 도움<br>

앞서 다음과 같은 문제를 받고나서 무작정 코드를 쓰기 전 아이디어를 작성해보았다.<br>
캐릭터가 살아 있는지 확인을 어떻게 할 것인지, 함수는 어떤걸 쓸 것인지 등 구상한 후 코드를 작성했다.<br>

# __init__ 게임 캐릭터 클래스
def __init__(self, name, hp, power):
        self.name = name
        self.hp = hp
        self.power = power

캐릭터를 효율적으로 받아올 수 있음<br>

# __is_alive__ 게임 캐릭터 생사 여부
살아있는지 확인하기 위해 self.hp가 0보다 크고 작음을 기준으로 하기로 했다.<br>
if self.hp > 0:<br>
            pass<br>
        else:<br>
            return f"{self.name}님은 이미 죽었습니다."<br>
이게 처음 짠 코드이고, 후에 get_attacked 함수에서 TRUE라는 값을 반환받아야 하기 때문에<br>
if self.hp > 0:<br>
            return True<br>
        else:<br>
            return False<br>
로 변경했다.<br>

# get_attacked 캐릭터의 체력을 깍는 함수
가장 어려웠던 코드.<br>
![맨 처음 짠 코드](https://github.com/Jinwo0o-develop/2025-06-08/blob/main/%EB%A7%A8%EC%B2%98%EC%9D%8Cget.png?raw=true)<br>
is_alive 함수를 기준으로 하고 싶은데 아직 인스턴스, 메소드 이런게 전부 어색하다보니 실수를 했다.<br>
아직 배움초반이기 때문에 더 많이 노력해보고 확실한 개념을 잡아야 할 필요가 있겠다고 느꼈다.<br>
머리속으로는 TRUE라는 값을 반환해주면 그걸 기준으로 조건을 나누고 싶었다.<br>
true 즉, 살아있으면 self.hp -= damage 수행, false면 "게임오버" 같은 방식으로 나누려고 했다.<br>
![중간수정](https://github.com/Jinwo0o-develop/2025-06-08/blob/main/%EC%88%98%EC%A0%95get_attacked.png?raw=true)<br>

# attack 함수와 __str__ 함수
![](https://github.com/Jinwo0o-develop/2025-06-08/blob/main/attack%20%ED%95%A8%EC%88%98%EC%99%80%20str.png?raw=true)<br>

# 첫번째_실행
character_1 = GameCharacter("Ww영훈전사wW", 200, 30)<br>
character_2 = GameCharacter("Xx지웅최고xX", 100, 50)<br>

character_1.attack(character_2)<br>
character_2.attack(character_1)<br>
character_2.attack(character_1)<br>
character_2.attack(character_1)<br>
character_2.attack(character_1) #여기서 character_1 사망<br>
character_2.attack(character_1)<br>

위 코드를 실행해보니 영훈전사의 hp는 -50으로 나왔다.<br>
내가 바라는 결과는 다음과 같았다.<br>
Ww영훈전사wW님은 이미 죽었습니다.<br>
Ww영훈전사wW님의 hp는 0만큼 남았습니다.<br>
Xx지웅최고xX님의 hp는 70만큼 남았습니다.<br>
<br>
즉, return 값으로 반환했으나 코드가 작동하지 않았다는 것<br>
<br>
# 수정
![GPT를 사용하던 방식](https://github.com/Jinwo0o-develop/2025-06-08/blob/main/GPT-%EC%84%A4%EC%A0%952.png?raw=true)<br>
![답](https://github.com/Jinwo0o-develop/2025-06-08/blob/main/GPT-%EB%8B%B5.png?raw=true)<br>
![](https://github.com/Jinwo0o-develop/2025-06-08/blob/main/GPT-%EC%84%A4%EC%A0%95.png?raw=true)<br>
<br>
내가 목표로 하는건 나 자신의 능력향상이였기 때문에, GPT를 사용할 때 위의 사진과 같은 방법을 두고 실행해왔다.<br>
![해결](https://github.com/Jinwo0o-develop/2025-06-08/blob/main/return%EB%AC%B8%20%EB%B2%84%EB%A6%87%EA%B3%BC%20%EC%9E%84%EC%8B%9C%EB%B0%A9%ED%8E%B8.png?raw=true)<br>
다음 사진처럼 실행하니 원하는 결과는 나왔었다.<br>
![GPT의 질문](https://github.com/Jinwo0o-develop/2025-06-08/blob/main/GPT%EC%9D%98%20%EC%A7%88%EB%AC%B8.png?raw=true)<br>
GPT가 다시 나에게 물었다<br>
self.hp = 0 이라는 코드가 작동하지 않았었기에, 기억 좀 하라고 명시하고 싶어서 썻다고 답했고, 이미 self.hp = 0 에서 기억하고 있으니 필요없는 코드라고 이야기 해주었다.<br>
이 문맥에서 내가 짠 코드에 부족한 점이 없는지, 더 나아질 코드가 있지 않을지 찾기 시작했다.<br>
아직 아는게 없어도 다 의심해보고 계속해서 체크해보았으며, 그 결과로 코드를 한번 더 수정할 수 있었다.<br>
![완료](https://github.com/Jinwo0o-develop/2025-06-08/blob/main/%EC%B5%9C%EC%A2%85%EC%88%98%EC%A0%95%EC%99%84%EB%A3%8C.png?raw=true)<br>
훨씬 더 깔끔하고 보기 좋은 코드를 완성했고, 솔직히 정말 진이 빠졌다.<br>
그래도 완성하니 정말 행복했다 <br>
몇시간 잡고 끝끝내 잡다보니 나와서 바로 침대에 누워서 쉬어버렸지만 역시 재밌다고 느낀 하루였다.<br>
