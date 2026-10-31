# Changelog — HomeNetwork fork (Lu1City SKLeadersView2nd / Sojulab)

## v1.4.0 (2026-10-30)
### Added
- **환기 전열교환기 바이패스(bypass) 지원** — RS-485 실차 관측 기반(2026-10-30 스니핑)
  - `PacketParser.handleVentilator`: `packet[8]` bit7(0x80) = 바이패스 플래그 파싱 → `result['bypass']`
  - `Ventilator.updateState/publishMQTT`: 상태 JSON에 `"bypass": 0|1` 추가
  - `Ventilator.makePacketSetBypass`: `F7 0B 01 2B 02 40 11 81/01 00 XX EE` (0x81=ON+바이패스 / 0x01=정상 전열교환)
  - `ThreadCommandQueue.set_ventilator_bypass`: ACK 확인 루프 포함 (state=ON & bypass 확인)
  - `Home.onMqttCommandVentilator`: `home/command/ventilator/<room>/<idx>` 의 `{"bypass":1|0}` 접수 ( 꺼져있으면 ON+모드 조합으로 전송)
  - HA MQTT discovery: `fan` 엔티티에 `preset_modes: [normal, bypass]` 추가 — HA UI 프리셋 드롭다운으로 제어
### Verified
- 2026-10-30 RS-485 120초 실관측: OFF(0x02)/ON(0x01)/BYPASS(0x81) + 풍량(0x01약/0x07강) 초 단위 일치
- 꺼짐예약(30/60/90분)은 버스 트래픽 없음 → 월패드 내부 타이머로 판정 (HA는 automation으로 대체 가능)
- XOR 체크섬 로직 실차 패킷과 전수 일치 확인

## v1.3.x 및 이전
- YOGYUI upstream 기반 (`Hillstate-Gwanggyosan` → `Lu1City-SKLeadersView2nd` 디렉터리 명명 포함)
- 0x75 디밍 그리드 8단계 fix (`fix/dimming-0x75` merge, 98ae44f)
