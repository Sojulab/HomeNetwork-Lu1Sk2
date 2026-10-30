# HomeNetwork (Fork — 루원시티 2차 SK 리더스뷰 아파트용)

이 포크는 **인천 루원시티 2차 SK 리더스뷰 아파트**의 월패드 환경에 맞춰 제작/검증된 HomeNetwork입니다.

## 이 포크의 특징
- **디밍 프로토콜 실측 adaptation**: 거실 디밍등은 `0x42`가 아닌 **서브주소 `0x75`**를 사용 (밝기 byte = 레벨×31, 8단계 그리드) — RS-485 버스 라이브 캡처 및 주입 테스트로 실증
- `fix/dimming-0x75` 브랜치: `DimmingLight.py` / `PacketParser.py` / `ThreadCommandQueue.py` 수정 (0x75 송수신 + 그리드 디코딩 + ON 시 밝기 단위 버그 수정)
- 원본: [YOGYUI/HomeNetwork](https://github.com/YOGYUI/HomeNetwork)

## 사용
HomeAssistant 애드온 [homeassistant-addons-Lu1Sk2](https://github.com/Sojulab/homeassistant-addons-Lu1Sk2)의 `branch_name: fix/dimming-0x75` 설정과 함께 사용합니다.
