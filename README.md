#### Provider 데이터 상태관리를 통해 Chart 및 Calendar 시각화

#### 사용 package: "Provder", "fl_chart"

#### 6/9 COMMIT

- 차트 데이터 입력 10개 이상 넘어가는 데이터는 차트UI에서 지워짐
- 차트 설명란, 캘린더 디자인 UI 개선

사용패키지:

- fl_chart: ^0.67.0
- intl: ^0.19.0
- provider: ^6.1.2
- table_calendar: ^3.1.1

---

#### Provider 코드블록

사용자 입력처리 받은 건강 정보(HealthData)를 List 형식의 Provider에서 상태관리.

```dart
class HealthDataProvider with ChangeNotifier {
  final List<HealthData> _healthDataList = []; // HealthData 객체 저장 리스트

  List<HealthData> get data => _healthDataList;

  void addHealthData(HealthData data) {
    _healthDataList.add(data);
    debugPrint('입력받음 : ${data.date.day}');
    notifyListeners();
  }

  List<HealthData> getDataForDay(DateTime day) {
    return _healthDataList.where((data) {
      // 세 조건 모두 참이면, 해당 data 객체는 결과 리스트에 포함된다,
      return data.date.year == day.year && data.date.month == day.month && data.date.day == day.day;
    }).toList();
  }
}

```

<hr>

#### Chart

코드의 중복을 줄이고, 간결하고 재사용성 있게끔 코드 메서드 분리
HealthDataProvider에 데이터를 읽고 차트로 시각화.

1. chart_page.dart
2. line_chart.dart

🔵 수축기선 / 🔴 이완기선 / 🟣 혈당선 / 🟢 각 적정선  
<img width="270" alt="image" src="https://github.com/alscks6521/fl_chart_analyze/assets/112923685/555beb8e-718f-4d7b-bcf2-f7536dc5d0f1">

<hr>

#### Calendar

HealthDataProvider에 데이터를 읽고 캘린더로 시각화.  
<img width="270" alt="image" src="https://github.com/alscks6521/fl_chart_analyze/assets/112923685/23d2412a-39ab-4faa-af7a-60a2b9d85996">
