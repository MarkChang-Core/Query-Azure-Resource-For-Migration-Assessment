## 匯出當前Azure中所有資源清單

由於當前許多MOLP、PAYG的使用者需要將資源遷移至CSP時，均會需要針對現有資源評估是否支援「跨訂閱遷移」，

因此以下步驟提供使用者針對「跨訂閱遷移評估」時，可透過匯出Azure現有的Resource清單，以加入進行評估作業。

--------------------------------

Step 1. 登入Azure Portal後，選擇當前訂用帳戶 – 

![GITHUB](https://github.com/MarkChang-Core/Query-Azure-Resource-For-Migration-Assessment/blob/main/image/image1.jpg)<br>

Step 2. 點擊當前需要移轉的訂用帳戶 – 

![GITHUB](https://github.com/MarkChang-Core/Query-Azure-Resource-For-Migration-Assessment/blob/main/image/image2.jpg)<br>

Step 3. 選擇導覽列中的 設定(Setting) > 資源(Resource)，並選擇上方的「建立查詢(Open query)」 – 

![GITHUB](https://github.com/MarkChang-Core/Query-Azure-Resource-For-Migration-Assessment/blob/main/image/image3.jpg)<br>

Step 4. 於Query KQL指令中輸以下指令，並執行 執行查詢(Run query) –

```
Resources
| where subscriptionId =~ "c71720d7-af16-48de-98e7-ffbcf15c7861"
| extend publisher = properties.storageProfile.imageReference.publisher
| extend offer = properties.storageProfile.imageReference.offer
| extend sku = properties.storageProfile.imageReference.sku
| project type, name, publisher, offer, sku
```

※ 其中 subscriptionId 請更換為當前之訂用帳戶ID
※ Query過程中，若畫面凍結無法繼續時，請重新整理後，再次輸入以下指令

![GITHUB](https://github.com/MarkChang-Core/Query-Azure-Resource-For-Migration-Assessment/blob/main/image/image4.jpg)<br>

Step 5. 完成Query後，請將「格式化結果(Formatted results)」切換為「關閉(off)」後，點選「Download as CSV」 -

![GITHUB](https://github.com/MarkChang-Core/Query-Azure-Resource-For-Migration-Assessment/blob/main/image/image5.jpg)<br>

最後，將匯出之 .csv 檔案提供給予CSP，即可協助進行資源跨訂閱遷移的評估，當然也可以透過Microsoft提供的[移動資源清單](https://docs.microsoft.com/zh-tw/azure/azure-resource-manager/management/move-support-resources)進行評估。
