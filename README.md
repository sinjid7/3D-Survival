죄송합니다.
제가 지난 주에 개인 일정으로 수업을 전체 불참하여 진도가 늦어지는 바람에 숙련 강의를 아직 완강하지 못하였습니다. 남은 주말 동안 열심히 공부 하도록 하겠습니다.
비록 아직 강의를 따라가는 중이지만 그 사이에 겪은 오류와 해결하는 과정을 서술해 보도록 하겠습니다.
트러블 슈팅
-플레이어 상태 및 UI 과정에서 hunger가 서서히 다 떨어진 후 health가 닳아야 하는 상황인데, hunger가 플레이 시작하자마자 0이 되고 health는 그대로인 오류가 발생
-스크립트를 다시 써보고 유니티에서 hunger를 조절해도 그대로인 상황 
-팀원들의 도움으로 플레이이어컨디션 스크립트에서 부등호를 등호로 바꾸고, Add와 Subtract에서 +,- 삭제 후 해결

//PlayerCondition 스크립트
private void Update()
{
    hunger.Subtract(hunger.passiveValue * Time.deltaTime);
    stamina.Add(stamina.passiveValue * Time.deltaTime);

    if (hunger.curValue <= 0f)
    {
        health.Subtract(noHungerHealthDecay * Time.deltaTime);
    }

    if (health.curValue <= 0f)
    {
        Die();
    }
}

//Condition 스크립트
 public void Add(float value)
 {
     curValue = Mathf.Min(curValue + value, maxValue);
 }

 public void Subtract(float value)
 {
     curValue = Mathf.Max(curValue - value, 0);
 }
