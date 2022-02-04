# Datepicker

공식문서 : https://reactdatepicker.com/

시작/끝나는 날 선택 및 지정해주는 기능을 사용하기 위해서 datepicker라는 달력 라이브러리를 사용했당.

- 설치방법 : npm install react-datepicker --save

참고로 import 해줄 때
**'react-datepicker/dist/react-datepicker.css'**
라는 css파일도 같이 불러와야 달력이 제대로 뜬다..

-사용방법

```
const DatePickerComponent = () => {
  const [startDate, setStartDate] = useState(new Date());

  return (
    <DatePicker
      selected={startDate}
      onChange={date => setStartDate(date)}
    />
  );
};
```

datepicker은 커스텀이랑 재사용이 쉬워서 필요한 기능들을 거의 다 가져다 쓰면 된다.

### startDate={new Date()}/minDate={startDate}

- 선택할 수 있는 날이 오늘 이전이 되지 않도록 new Date()를 써주고 끝나는 날은 시작하는 날 이전이 안되도록 설정해줬다.
