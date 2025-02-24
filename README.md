# 바닐라 JS 프로젝트 성능 개선
- url: https://d2bs5sb8hgr7py.cloudfront.net/

## 성능 개선 보고서

### 1. 개선 이유
1️⃣ 이미지 형식 변환으로 최적화 (JPG → WebP) 
  - 이미지 형식을 JPG에서 WebP로 변환하여 LCP(Largest Contentful Paint) 성능을 개선하고자 했습니다.
  - WebP는 더 나은 압축률을 제공하며, 파일 크기를 줄이면서도 고화질을 유지할 수 있어 로딩 시간이 단축됩니다.

2️⃣ Google Heebo 폰트 최적화 
  - 폰트 로딩 시간을 단축시키고 FCP(First Contentful Paint)와 CLS(Cumulative Layout Shift)를 개선하기 위해 Google Heebo 폰트를 자체 호스팅으로 변경하였습니다.
  - 최적화된 WOFF2 형식으로 교체하여 로딩 속도와 레이아웃 안정성을 향상시켰습니다.

3️⃣ 제품 이미지 Lazy Loading 적용 
  - 초기 페이지 로딩 시간을 단축하고 LCP를 개선하기 위해 제품 이미지를 Lazy Loading 방식으로 적용했습니다.
  - 이를 통해 뷰포트 내에서만 이미지가 로드되어 초기 로딩 성능을 높일 수 있었습니다.

4️⃣ 명시적 이미지 크기 설정 및 스켈레톤 적용 
  - CLS를 개선하고 레이아웃 안정성을 높이기 위해 모든 이미지에 명시적 크기(width, height)를 설정하고,
    이미지 로딩 전에 스켈레톤 UI를 적용하여 이미지가 로드될 때 발생할 수 있는 레이아웃 이동을 최소화했습니다.

5️⃣ 중요하지 않은 스크립트 지연 로딩 
  - 초기 페이지 로딩 속도를 개선하기 위해 비필수적인 스크립트에 defer 속성을 추가하여, 페이지의 중요한 콘텐츠가 먼저 로딩되도록 하였습니다.
  - 이를 통해 렌더링 차단을 최소화하고 사용자 경험을 개선했습니다.

6️⃣ Products에 `picture`, `source` 태그 추가 
  - 다양한 디바이스와 화면 크기에서 최적화된 이미지를 제공하기 위해 `picture` 및 `source` 태그를 활용하여 고해상도와 다양한 형식(WebP, JPG 등)
    이미지를 기기와 네트워크 환경에 맞게 자동으로 로딩하도록 했습니다.

7️⃣ 스크립트 최적화 작업 
  - 전체적인 자바스크립트 실행 성능을 향상시키기 위해 불필요한 코드 제거 하여 스크립트 실행 시간을 줄였습니다.


### 2. 개선 방법
1️⃣ 이미지 형식 변환으로 최적화 (JPG → WebP) 
  - 기존의 JPG 이미지를 WebP 형식으로 변환하여 사용했습니다.
  - WebP 형식은 고효율적인 압축 방식으로, 이미지 품질을 유지하면서 파일 크기를 줄일 수 있어 페이지 로딩 성능을 향상시켰습니다.

2️⃣ Google Heebo 폰트 최적화 
  - Google Heebo 폰트를 자체 호스팅하여 의존도를 줄였으며, WOFF2 형식으로 변경하여 로딩 속도를 개선했습니다.
  - 이 방식은 폰트 파일 크기도 작아지고, 다양한 디바이스에서의 로딩 성능도 향상시켰습니다.

3️⃣ 제품 이미지 Lazy Loading 적용 
  - 이미지 요소에 loading="lazy" 속성을 추가하여 뷰포트 밖에 있는 이미지는 사용자가 스크롤을 내릴 때까지 로딩을 지연시켰습니다.
  - 이를 통해 초기 로딩 시 불필요한 이미지 로딩을 지연시켜, LCP 개선에 도움을 주었습니다.

4️⃣ 명시적 이미지 크기 설정 및 스켈레톤 적용 
  - 모든 이미지에 width와 height 속성을 명시적으로 지정하여 레이아웃 변화를 방지하고,
  - 이미지가 로딩되기 전에는 스켈레톤 UI를 표시하여 사용자에게 로딩 상태를 명확히 전달했습니다.

5️⃣ 중요하지 않은 스크립트 지연 로딩 
  - 스크립트에 defer를 추가하여, 초기 콘텐츠가 먼저 렌더링되고 자바스크립트 로딩이 후속적으로 이루어지도록 하였습니다.
    이를 통해 초기 렌더링 성능을 최적화했습니다.

6️⃣ Products에 `picture`, `source` 태그 추가 
  - `picture`와 `source` 태그를 사용하여 다양한 해상도에 맞는 이미지를 제공하고, WebP 형식과 JPG 형식을 동시에 제공하여,
     고화질 이미지를 효율적으로 로딩할 수 있도록 했습니다.

7️⃣ 스크립트 최적화 작업 
  - 자바스크립트 코드에서 불필요한 코드를 제거하고, 코드 압축 및 최소화를 적용하여 파일 크기를 줄여 성능을 개선했습니다.


### 3. 개선 후 향상된 지표
   
| 개선 전            | 개선 후 |
|--------------------------|-------------|
| ![image](https://github.com/user-attachments/assets/763b9df3-5e79-42ac-b04a-063ff0a37ff5) | ![image](https://github.com/user-attachments/assets/11d36014-4fa0-42d3-a24f-197b72d2daac)|


| 측정 지표  | 개선 전 | 개선 후 | 개선율 (%) |
|----------|-------------|-------------------|-----------|
| 성능  | 65 | 99 | **52%** |
| 접근성  | 82 | 95 | **16%** |
| 검색엔진 최적화  | 82 | 91 | **11%** |
| FCP(First Contentful Paint)  | 800ms | 300ms | **63%** |
| LCP(Largest Contentful Paint) | 2300ms | 900ms | **61%** |
| TBT(Total Blocking Time) | 80ms | 80ms | **0%** |
| CLS(Cumulative Layout Shift) |  0.513 | 0.016 | **97%** |
| Speed Index |  1100ms | 800ms | **27%** |


### 4.  분석 및 결론
  - 전체 성능 점수 향상 : 
      Lighthouse 성능 점수가 65에서 99로 52% 증가하여 웹사이트의 전반적인 성능이 크게 개선되었습니다.
  - 로딩 속도 개선 : 
      FCP가 63%, LCP가 61% 개선되어 사용자가 콘텐츠를 더 빠르게 볼 수 있게 되었습니다.
      특히 LCP가 2300ms에서 900ms로 줄어들면서, 사용자들이 콘텐츠를 더 빠르게 접근할 수 있게 되었습니다. 
  - 레이아웃 안정성 향상 : 
      CLS가 0.513에서 0.016으로 97% 개선되어 페이지 로딩 중 레이아웃 이동이 거의 없어졌습니다.
  - 접근성 및 SEO 개선 : 
      접근성 점수가 16%, SEO 점수가 11% 향상되어 더 넓은 사용자층에게 접근 가능하고 검색 엔진에 최적화된 웹사이트가 되었습니다. 


   
## 과제 회고
성능 개선 작업을 진행하면서 웹 최적화의 중요성을 직접 체감할 수 있었고, 다양한 방법을 실험하고 적용하는 과정에서 많은 것을 배울 수 있었습니다.
특히, LCP, FCP, CLS와 같은 핵심 성능 지표를 분석하고 개선하는 과정을 통해, 각각의 지표에 어떤 최적화 전략이 효과적인지 이해할 수 있었습니다. 

또한, 이미지 최적화(WebP 변환, Lazy Loading, picture 태그 활용)와 폰트 최적화(자체 호스팅, WOFF2 적용)가 실제로 로딩 속도 개선에 큰 영향을 미친다는 점을 직접 확인할 수 있었고,
불필요한 스크립트 로딩을 지연(defer 적용)하고, 명시적으로 이미지 크기를 지정하는 방식이 렌더링 차단을 최소화하고 레이아웃 안정성을 높이는 데 효과적이라는 점도 배울 수 있었습니다.

이번 경험을 통해 단순히 기능 구현을 넘어서, 사용자가 더 빠르고 쾌적하게 웹을 이용할 수 있도록 고민하는 과정이 중요하다는것을 다시 한번 깨닫게 되었던것 같습니다.
앞으로도 지속적으로 성능 최적화에 대한 학습을 이어가며, 더 나은 사용자 경험을 제공할 수 있도록 노력하려합니다!
