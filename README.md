# Mealy 상태 머신 · LAB2

학생용 시작점은 빈 템플릿 v2.0.0이다. 이 폴더는 강사용 완성 코드 예시를 제작 중인 작업본이다.

```powershell
git clone --branch v2.0.0 https://github.com/Glaysia/fpga-lab-template.git lab2_07_mealy
cd lab2_07_mealy
git switch -c main
code LAB1.code-workspace
```

기능 코어: `mealy_toggle` / Vivado 설계 top: `lab2_mealy` / 시뮬레이션 top: `tb_mealy_toggle`.

- `src/mealy_toggle.v`: 직접 학습하는 회로.
- `src/input_frontend.v`: 리셋 해제 동기화, 두 단계 입력 동기화, 20 ms 버튼 디바운스와 한 클록 펄스.
- `src/lab2_mealy.v`: 입력·출력을 코어와 보드 핀 이름에 연결.
- `sim/tb_mealy_toggle.sv`: 기능 코어의 자기검사. 보드 핀 검증과 구분한다.
- `constraints/lab2_mealy.xdc`: 19개 포트, S75 핀과 LVCMOS33, 1 kHz 주 클록 제약.

장비 설정: 주 클록을 **1 kHz**로 설정하고 초기화 버튼 K4를 누른 뒤 놓는다. 버튼 N8은 클록이 아니라 입력이다. 스위치를 먼저 정하고 버튼을 누른다.

SW1(sw[7]): 입력. 1에서 버튼을 누르면 상태 전환. 버튼 없이 SW1을 바꿔도 동기화 지연 후 출력 변화. LED[2]=상태, LED[1:0]=출력.

입력 동기화 때문에 버튼과 DIP 입력은 즉시 반영되지 않는다. 버튼은 누름과 뗌 모두 충분한 안정 시간이 필요하다. 기계적 접점과 메타안정성의 실제 특성은 기능 시뮬레이션만으로 증명하지 않는다.

실행: Terminal → Run Task... → 02 Simulate. 보드 연결 검증 및 실제 장치 실행 상태는 상위 LAB2 검증 기록을 확인한다.
