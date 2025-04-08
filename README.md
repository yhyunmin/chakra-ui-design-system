# Chakra UI 디자인 시스템 

## -
Chakra UI를 기반의 디자인시스템을 Storybook 을 통해 컴포넌트를 시각화, 문서화한 프로젝트 입니다.   
프로젝트를 통해 개발자와 디자이너 간의 작업을 쉽게 진행 할 수 있습니다.

## -
* 반복적으로 사용하는 UI 요소들을 컴포넌트로 만들어 개발 속도를 높입니다.
* 새로운 컴포넌트를 쉽게 추가할 수 있도록 구조를 유연하게 구성합니다.

## 기술스택

* React,Typescript
* Styled Components / sass(alternative)
* Storybook
* Turborepo,pnpm
* SLACK / GITHUB 

## 개발서버 실행
```

# 스타일드 컴포넌트 스토리북 실행
pnpm storybook:styled

```

## 프로젝트 구조 

```
├── packages/
│   ├── chakra-ui-styled/             # styled-components 기반 디자인 시스템
│   │   ├── src/
│   │   │   ├── components/           # 컴포넌트 코드
│   │   │   ├── foundation/           # 디자인 기초 요소
│   │   │   └── hooks/                # 커스텀 훅
│   ├── typescript-config/            # monorepo TS
│   ├── eslint-config/                # monorepo ESLint
│   └── stylelint-config/             # monorepo StyleLint
├── apps/
│   └── team-styled/                    # 스타일드 컴포넌트 기반 스토리북
```

## 주요 컴포넌트

* 레이아웃 컴포넌트
> Box,Flex,Grid,Container 등 기본 레이아웃 요소가 포함 되어 있습니다.
* 폼 컴포넌트
> Button,Input,Checkbox,Radio,Select,Switch 등 인터랙션 요소가 포함되어 있습니다. 
* 피드백 컴포넌트
> Alert,Toast,Progress,Spinner 등 상태 관련 요소가 포함되어있습니다.
* 네비게이션 컴포넌트
> Menu,Tabs,Breadcrumb,pagination 등 네비게이팅 시스템 요소가 포함되어 있습니다.
* 데이터 표시 컴포넌트
> Badge,Card,List,Table 등 정보 표시 요소가 포함되어 있습니다. 

## 디자인 토큰 시스템
> 파운데이션 중 토큰은  아래와 같이 체계화 하였습니다.

* 색상 시스템
> 브랜드 컬러, 시맨틱 컬러, 그레이스케일로 구성되어있습니다 50~900 까지 Shade 구성하였습니다.
* 타이포그래피
> 헤딩과 본문용으로 스타일 구분하였습니다.
* 여백 / 레이아웃
> 간격을 일관되게 해 컴포넌트 간 통일감을 구성하였습니다. 


## 개발 과정 중 고민

1. 컴포넌트 설계
```
<Button 
  size="md"
  colorScheme="blue"
  variant="outline"
  leftIcon="search"
  isLoading={false}
>
  검색하기
</Button>
```
props 네이밍과 기본값 설정의 중점을 둬 컴포넌트의 구성을 빠르게 확인하려 했고,
컴포넌트 코드를 따로 확인 하지 않고도 좀더 쉽게 이해할수 있도록 작업했습니다.

2. 타입 정의
타입스크립트를 도입하여, 자동완성과 타입검사를 가능하게 했는데요. 타입 체크를
엄격하게 구현하여 types 확인으로 하나의 문서처럼 확인할 수 있도록 구성하였습니다.

3. 테마 시스템
```
const Button = styled.button<ButtonProps>`
  padding: ${({ theme, size }) => theme.spacing[size]};
  background-color: ${({ theme, colorScheme }) => theme.colors[colorScheme][500]};
  color: ${({ theme }) => theme.colors.white};
  border-radius: ${({ theme }) => theme.radii.md};
  // ...
`;
```
전체 디자인을 변경할 수 있는 상황을 고려하여 확장성을 생각해 전체적인 스타일링을 토큰을 적극 활용하였습니다.

4. 폴더 구조
```
components/
  └── button/
      ├── Button.tsx         # 기본 컴포넌트
      ├── Button.styles.ts   # 스타일 정의
      ├── Button.types.ts    # 타입 정의
      ├── Button.stories.tsx # 스토리북 문서
      ├── Button.test.tsx    # 테스트 코드
      └── index.ts           # exports 
```
storybook 외에도 폴더트리내에서도 컴포넌트 구성을 알 수 있도록 컴포넌트 마다 독립적인 폴더를 가져  관련파일을 같이 구성하도록 하였습니다.


## 개선 방향
* 접근성을 고려하여 모든 사용자에게 동일한 사용감을 개선 해야합니다. 
> 접근성 개발