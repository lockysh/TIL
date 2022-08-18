# FlatList
오직 현재 화면에 보여지는 요소들만 렌더링 하며 데이터가 많아서 표현해야 할 요소가 많은 리스트에서 사용한다.

```
const App = () => {
  const renderItem = ({item}: any) => <Item title={item.title} />;

  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={DATA}
        renderItem={renderItem}
        keyExtractor={item => item.id}
      />
    </SafeAreaView>
  );
};
```

### Props

- renderItem과 data는 필수적으로 사용해야되는 Props이다.

- extraData : 리스트에 리렌더링을 알려주기 위한 마커 프로퍼티

- onEndReached :
  사용자가 목록 끝에 도달하여 새로운 것들을 로드해야할 때 실행되는 함수.
  이 prop을 사용하여 infinite scroll을 간단하게 구현할 수 있다.

- onEndReachedThreshold :
  onEndReached를 실행시키려는 목록의 하단에서 내용의 끝까지의 거리. (default = 0.5, 숫자가 작을수록 더 아래에서 실행됨)

## SectionList

- FlatList와 동일하지만 Section을 표현할 수 있는 List Component

```
<SectionList
    sections={DATA}
    keyExtractor={(item, index) => item + index}
    renderItem={({ item }) => <Item title={item} />}
    renderSectionHeader={({ section: { title } }) => (
      <Text style={styles.header}>{title}</Text>
    )}
/>
```

- renderSectionHeader Props를 통해서 Section을 표현할 수 있다.
