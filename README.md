# Logistics_Optimization
물류 최적경로 도출  
부품을 보관하는 창고에서 생산 공장으로 부품 운송  
<img width="190" alt="image" src="https://user-images.githubusercontent.com/24906028/179396261-bf14a71d-c242-4a34-8a69-46c79ad835b6.png">
남부공장이 효율 높게 부품을 운송하고 있다.  
<img width="325" alt="image" src="https://user-images.githubusercontent.com/24906028/179396356-21f4fecd-383f-4653-96d0-c6ad86bac18e.png">
어느 창고에서 어느 공장으로든 골고루 운송경로가 보인다.  
운송 비용을 생각하면 운송 경로는 어느정도 집중되는 편이 효율적일 것이다.  
<img width="101" alt="image" src="https://user-images.githubusercontent.com/24906028/179396453-eb961d8d-1587-4a5f-ac40-183d6cc204d0.png">
최적화 전 총 운송비용
<img width="211" alt="image" src="https://user-images.githubusercontent.com/24906028/179396580-f0b62741-79ca-4ae2-8365-7e51aa4118bb.png">
최적화 전에는 제약조건을 모두 만족하고 있다.
<img width="91" alt="image" src="https://user-images.githubusercontent.com/24906028/179396631-f6e48f01-9b6d-47ab-a09d-63cd5d9d5157.png">
<img width="133" alt="image" src="https://user-images.githubusercontent.com/24906028/179396607-8affb6d9-f222-49e3-8b29-6760249739a4.png">
운송경로 변경 시 총 운송비용은 줄어들 수 있으나 제약조건을 만족하지 못할 수 있다.

## 라이브러리를 활용한 물류 네트워크 최적화
최종적으로 제품을 판매하는 대리점(P, Q)  
판매되는 상품군(A, B) -> 일정 수요가 예측되어 있음  
수요량을 근거로 공장(X, Y)에서의 생산량 결정  
각 제품을 어느 생산라인(0, 1)에서 제조할지에 대해서는 각 공장에서 대리점까지의 운송비, 재고 비용 등을 고려해서 결정  
pulp -> 최적화 모델  
ortoolpy -> 목적함수를 생성해서 최적화 문제 푸는 역할  
### 최적화 결과
<img width="130" alt="image" src="https://user-images.githubusercontent.com/24906028/179397141-e31aabaf-65c0-4672-854c-31b6c60bc526.png">
<img width="311" alt="image" src="https://user-images.githubusercontent.com/24906028/179397161-103e01e4-af2a-431b-849f-008ba4e933d3.png">
기존보다 운송경로가 집중됨.  

## 운송 비용뿐만 아니라 생산계획도 최적화
<img width="146" alt="image" src="https://user-images.githubusercontent.com/24906028/179397283-afcda075-10c9-4050-8f2a-4362476da0fa.png">
<img width="80" alt="image" src="https://user-images.githubusercontent.com/24906028/179397356-f038ecfe-b4c3-4265-908a-a19b5a4827b7.png">
이익이 큰 제품1만 생산하고 있으며 원료가 효율적으로 사용되지 않고 있음
### 최적화 결과
<img width="90" alt="image" src="https://user-images.githubusercontent.com/24906028/179397373-bcf5e03d-0f69-4d3f-bf0a-316da654a9de.png">
<img width="175" alt="image" src="https://user-images.githubusercontent.com/24906028/179397386-3f2f9b72-26c7-4bfb-b0e8-f9e0d97973be.png">
제약조건을 모두 충족하면서 원료 1이 조금 남아있기는 하지만 최전화 전과 비교하면 원료를 효율적으로 사용한다.
## 운송경로와 생산계획 동시에 고려하기
운송비용과 제조비용이 수요를 만족하면서 최소가 되게  
목적함수 -> 운송비용과 제조비용의 합  
제약조건 -> 대리점의 판매 수가 수요 수를 넘는 것  
ValY -> 최적 생산량  
ValX -> 최적 운송량
<img width="205" alt="image" src="https://user-images.githubusercontent.com/24906028/179397612-c7546162-a17a-4e54-8bfb-f2e059c2808c.png">
<img width="88" alt="image" src="https://user-images.githubusercontent.com/24906028/179397623-ca9bed95-74ef-49cd-a16c-81ce0e2dd2ee.png">
되도록 운송비가 적은 공장X-대리점P, 공장Y-대리점Q의 경로 사용
<img width="243" alt="image" src="https://user-images.githubusercontent.com/24906028/179397634-de2bbc02-f790-45bf-a5b2-1c870dc76e5b.png">
<img width="97" alt="image" src="https://user-images.githubusercontent.com/24906028/179397643-23dddbe4-df28-4728-9517-6a78500fdf35.png">
되도록 생산비용이 낮은 공장X에서의 생산량을 늘림. 하지만 운송비용까지 고려하면 수요량이 많은 대리점Q까지의 운송비용이 적은 공장Y를 어느 정도 가동시키지 않을 수 없다.
