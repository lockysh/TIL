# Animation
- react native 에서 touchableOpacity에 애니메이션 효과를 주는 경우, 1. 투명도를 바꾸는 애니메이션, 2. 실제 애니메이션 총 2개의 애니메이션을 실행해야하기 때문에 부자연스럽다. 따라서 View에 애니메이션 효과를 주는 것이 더 자연스럽다.

## rules

1. Animated.Value를 통해 원하는 value 값을 구해야함.
   (state 사용X)
2. value 값을 직접 설정하지 않고 Animated API를 사용해야함.
3. Animatable components에만 애니메이션이 적용가능함.
   => Animatable component가 아닌 컴포넌트에 애니메이션을 적용하고 싶을 경우 createdAnimatedComponent() 함수를 사용해야함.

- <3-1> styled-component를 사용하여 Animatable component가 아닌 컴포넌트를 사용가능하게 만드는 두가지 방법

1. const Box = styled(Animated.createAnimatedComponent(TouchableOpacity))`
2. 이미 생성된 styled component를 animated 컴포넌트에 넣어준다
   const AnimatedBox = Animated.createAnimatedComponent(Box);

## interpolation
