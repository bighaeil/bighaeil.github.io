---
title: "multi-columns - CSS 개인 공부 정리"
categories: 
  - css
last_modified_at: 2020-09-05T20:20:00
---

# multi-columns

일반 블록 레이아웃을 확장하여  
여러 텍스트 다단으로 쉽게 정리하며, 가독성 확보

[multi-column : mdn](https://developer.mozilla.org/ko/docs/CSS3_Columns)

## columns

다단을 정의 - 단축 속성

* 단축 속성 : 속성안 값이 여러개가 들어가고 띄어스기로 구분되며 각각 의미가 있다.

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| auto | 브라우저가 단의 너비와 개수를 설정 | 기본값 |
| column-width | 단의 최적 너비를 설정 |  |
| column-count | 단의 개수를 설정 |  |

```css
.text {
  columns: 너비 개수;
}
```

### column-width

단의 최적 너비를 설정 - 개별 속성

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| auto | 브라우저가 단의 너비를 설정 | 기본값 |
| 단위 | px, em, cm 등 |  |

각 단이 줄어들 수 있는 최적 너비(최소 너비)를 설정하며,  
요소의 너비가 가변하여 하나의 단이 최적 너비보다 줄어들 경우 단의 개수가 조정됨


### column-count

단의 개수를 설정 - 개별 속성

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| auto | 브라우저가 단의 개수를 설정 | 기본값 |
| 숫자 | 단의 개수를 설정 |  |

* column-width 와 column-count 는 최적의 너비와 개수를 제안하는 것이지 브라우저(화면)의 너비가 맞지 않은 경우(화면이 너 작은 경우) 갯수가 줄어들거나 너비가 줄어들 수 있다.

## column-gap

단과 단 사이의 간격 설정

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| normal | 브라우저가 단과 단 사이의 간격을 설정(1em) | 기본값 |
| 단위 | px, em, cm 등 |  |

* 1em 은 font-size 와 같다.


## column-rule

단과 단 사이의 (구분)선을 지정 - 단축 속성  
구분선(column-role)은 단과 단 사이의 간격 중간에 위치  

| 값 | 의미 | 기본값 |
|:---|:---|---:|
| column-width | 선의 두께를 지정 | medium |
| column-style | 선의 종류를 지정 | none |
| column-color | 선의 색상을 지정 | 요소의 글자색과 동일 |

```css
.text {
  column-rule: 두께 종류 색상;
}
```
* 구분선은 설정이 없는 경우 color (글자색)의 영향을 받는다. 


