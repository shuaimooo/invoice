<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LUMASONIX 技術人員報價單</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Add html2pdf library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@300;400;500;700&display=swap');
        
        body {
            font-family: 'Noto Sans TC', sans-serif;
            background-color: #f5f7fa;
        }
        
        .invoice-container {
            background-color: white;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        
        .invoice-header {
            background-color: #1a3a5f;
            color: white;
        }
        
        .form-input {
            border: 1px solid #e2e8f0;
            padding: 0.5rem;
            border-radius: 0.25rem;
            width: 100%;
        }
        
        .table-header {
            background-color: #1a3a5f;
            color: white;
        }
        
        .table-row:nth-child(even) {
            background-color: #f8fafc;
        }
        
        .table-row:hover {
            background-color: #edf2f7;
        }
        
        .terms-section {
            background-color: #f8fafc;
            border-left: 4px solid #1a3a5f;
        }
        
        @media print {
            body {
                background-color: white;
            }
            
            .invoice-container {
                box-shadow: none;
            }
            
            .no-print {
                display: none;
            }
        }
    </style>
</head>
<body class="p-4 md:p-8">
    <div id="invoice-content" class="invoice-container max-w-5xl mx-auto p-6 rounded-lg">
        <!-- Header -->
        <div class="flex flex-col md:flex-row justify-between items-center mb-6">
            <div class="mb-4 md:mb-0">
                <h1 class="text-2xl font-bold text-gray-800">LUMASONIX x PROFESSIONAL</1>
                <p class="text-gray-600">專業技術支援 x 人力媒合平台</p>
            </div>
            <div class="bg-gray-800 text-white py-2 px-4 rounded">
                <h2 class="text-xl font-bold">技術人員報價單</h2>
            </div>
        </div>
        
        <!-- Client Info -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
            <div class="grid grid-cols-3 gap-2">
                <div class="font-medium text-gray-700">廠商名稱:</div>
                <div class="col-span-2">
                    <input type="text" class="form-input" id="clientName">
                </div>
                
                <div class="font-medium text-gray-700">派遣日期:</div>
                <div class="col-span-2">
                    <input type="date" class="form-input" id="dispatchDate">
                </div>
                
                <div class="font-medium text-gray-700">活動地點:</div>
                <div class="col-span-2">
                    <input type="text" class="form-input" id="eventLocation">
                </div>
                
                <div class="font-medium text-gray-700">聯絡窗口:</div>
                <div class="col-span-2">
                    <input type="text" class="form-input" id="contactPerson">
                </div>
            </div>
            
            <div class="grid grid-cols-3 gap-2">
                <div class="font-medium text-gray-700">報價編號:</div>
                <div class="col-span-2">
                    <input type="text" class="form-input" id="quoteNumber">
                </div>
                
                <div class="font-medium text-gray-700">報價日期:</div>
                <div class="col-span-2">
                    <input type="date" class="form-input" id="quoteDate">
                </div>
                
                <div class="font-medium text-gray-700">負責人:</div>
                <div class="col-span-2">
                    <input type="text" class="form-input" id="responsiblePerson" value="蘇裕庭">
                </div>
                
                <div class="font-medium text-gray-700">聯絡電話:</div>
                <div class="col-span-2">
                    <input type="text" class="form-input" id="contactPhone" value="0926169899">
                </div>
            </div>
        </div>
        
        <!-- Invoice Items -->
        <div class="overflow-x-auto mb-6">
            <table class="w-full border-collapse">
                <thead>
                    <tr class="table-header">
                        <th class="py-2 px-4 text-left">品項</th>
                        <th class="py-2 px-4 text-center">數量</th>
                        <th class="py-2 px-4 text-center">單價 (NT$)</th>
                        <th class="py-2 px-4 text-left">工作內容</th>
                        <th class="py-2 px-4 text-right">小計 (NT$)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr class="table-row border-b">
                        <td class="py-2 px-4">人事支援</td>
                        <td class="py-2 px-4">
                            <input type="number" min="0" class="form-input text-center" id="staff-qty" value="0">
                        </td>
                        <td class="py-2 px-4 text-center">2,500</td>
                        <td class="py-2 px-4">進場、演出、撤場</td>
                        <td class="py-2 px-4 text-right" id="staff-total">0</td>
                    </tr>
                    <tr class="table-row border-b">
                        <td class="py-2 px-4">燈/音/視控</td>
                        <td class="py-2 px-4">
                            <input type="number" min="0" class="form-input text-center" id="control-qty" value="0">
                        </td>
                        <td class="py-2 px-4 text-center">1,000</td>
                        <td class="py-2 px-4">演出前一日彩排，將視為一場演出，另行計費。<br>彩排與演出同日進行，僅收取一次演出費用。</td>
                        <td class="py-2 px-4 text-right" id="control-total">0</td>
                    </tr>
                    <tr class="table-row border-b">
                        <td class="py-2 px-4">追光燈操作</td>
                        <td class="py-2 px-4">
                            <input type="number" min="0" class="form-input text-center" id="spotlight-qty" value="0">
                        </td>
                        <td class="py-2 px-4 text-center">1,000</td>
                        <td class="py-2 px-4">演出前一日彩排，將視為一場演出，另行計費。<br>彩排與演出同日進行，僅收取一次演出費用。</td>
                        <td class="py-2 px-4 text-right" id="spotlight-total">0</td>
                    </tr>
                    <tr class="table-row border-b">
                        <td class="py-2 px-4">高空作業</td>
                        <td class="py-2 px-4">
                            <input type="number" min="0" class="form-input text-center" id="height-qty" value="0">
                        </td>
                        <td class="py-2 px-4 text-center">1,000</td>
                        <td class="py-2 px-4">作業高度達layher第 6 格以上(約9米)</td>
                        <td class="py-2 px-4 text-right" id="height-total">0</td>
                    </tr>
                    <tr class="table-row border-b">
                        <td class="py-2 px-4">加班費用</td>
                        <td class="py-2 px-4">
                            <input type="number" min="0" class="form-input text-center" id="overtime-qty" value="0">
                        </td>
                        <td class="py-2 px-4 text-center">350</td>
                        <td class="py-2 px-4">依實際加班時數計算</td>
                        <td class="py-2 px-4 text-right" id="overtime-total">0</td>
                    </tr>
                    <tr class="table-row border-b">
                        <td class="py-2 px-4">跨縣市</td>
                        <td class="py-2 px-4">
                            <input type="number" min="0" class="form-input text-center" id="travel-qty" value="0">
                        </td>
                        <td class="py-2 px-4 text-center">300</td>
                        <td class="py-2 px-4">交通費</td>
                        <td class="py-2 px-4 text-right" id="travel-total">0</td>
                    </tr>
                    <tr class="table-row border-b">
                        <td class="py-2 px-4">行政執行費</td>
                        <td class="py-2 px-4 text-center">一式</td>
                        <td class="py-2 px-4 text-center">10%</td>
                        <td class="py-2 px-4">人事支援 x 10% x 2500</td>
                        <td class="py-2 px-4 text-right" id="admin-total">0</td>
                    </tr>
                    <tr class="table-row border-b">
                        <td class="py-2 px-4">其他</td>
                        <td class="py-2 px-4 text-center">一式</td>
                        <td class="py-2 px-4 text-center"></td>
                        <td class="py-2 px-4">
                            <input type="text" class="form-input" id="other-desc" placeholder="其他項目描述">
                        </td>
                        <td class="py-2 px-4">
                            <input type="number" min="0" class="form-input text-right" id="other-amount" value="0">
                        </td>
                    </tr>
                </tbody>
                <tfoot>
                    <tr class="bg-gray-100">
                        <td colspan="4" class="py-2 px-4 text-right font-bold">未稅金額:</td>
                        <td class="py-2 px-4 text-right font-bold" id="subtotal">NT$0</td>
                    </tr>
                    <tr class="bg-gray-800 text-white">
                        <td colspan="4" class="py-2 px-4 text-right font-bold">總計:</td>
                        <td class="py-2 px-4 text-right font-bold" id="total">NT$0</td>
                    </tr>
                </tfoot>
            </table>
        </div>
        
        <!-- Terms and Conditions -->
        <div class="terms-section p-4 mb-6">
            <h3 class="text-lg font-bold mb-2">【注意事項／條款說明】</h3>
            <ol class="list-decimal pl-5 space-y-1 text-sm">
                <li>本報價僅供雙方事前評估與確認服務內容之用，最終金額以實際執行後確認為準。一經貴公司確認排班並完成當日工作，即視同同意報價單全部條件。</li>
                <li>協力技術人員說明: 本人僅協助媒合與執行活動之統籌角色，執行風險與責任應由現場技術人員自負。</li>
                <li>特殊作業加價：施工期間需於Layher6格以上(約9米高)進行作業者，皆視為高空作業，並將另行計費。</li>
                <li>時間場次與交通補貼定義：
                    <ul class="list-disc pl-5 mt-1">
                        <li>第九個小時開始跳算加班,費用為 NT$350/小時。</li>
                        <li>移動至不同活動場地即視為新場次，費用重新計算。</li>
                        <li>非北北基作業每跨一縣市加收交通費 NT$300。</li>
                        <li>需配合至貴公司協助開立公司貨車前往活動現場，將另酌收 NT$500 元。</li>
                        <li>上下班工作時數計算，將以人員自公司出發至返抵公司之實際時間為準(含上下貨)。</li>
                    </ul>
                </li>
                <li>付款與取消/改期條款：演出當天取消需支付報價金額之 50% ，改期需於五日前通知，否則視同取消。</li>
                <li>驗收與交付確認：活動結束雙方應現場確認交付狀況後視驗收完畢，恕不再就當日服務異議減項。</li>
                <li>維持作業品質與人員安排效率包含人員排程統整、資料彙整確認、作業溝通、異動回報、明細核對等相關行政作業，凡協助媒合與統籌之專案，將酌收行政執行費用，已併入請款明細列示。</li>
            </ol>
            <p class="mt-3 text-sm font-medium">「本次為人力技術統籌協助性質，若需責任劃分或正式承攬合約，可另洽討論，可提供協力條款供參。」</p>
        </div>
        
        <!-- Action Buttons -->
        <div class="flex justify-end space-x-4 no-print">
            <button id="print-btn" class="bg-gray-600 hover:bg-gray-700 text-white py-2 px-4 rounded flex items-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 17h2a2 2 0 002-2v-4a2 2 0 00-2-2H5a2 2 0 00-2 2v4a2 2 0 002 2h2m2 4h6a2 2 0 002-2v-4a2 2 0 00-2-2H9a2 2 0 00-2 2v4a2 2 0 002 2zm8-12V5a2 2 0 00-2-2H9a2 2 0 00-2 2v4h10z" />
                </svg>
                列印報價單
            </button>
            <button id="reset-btn" class="bg-red-600 hover:bg-red-700 text-white py-2 px-4 rounded flex items-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15" />
                </svg>
                重置表單
            </button>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Set today's date as default
            const today = new Date().toISOString().split('T')[0];
            document.getElementById('quoteDate').value = today;
            
            // Add event listeners to all quantity inputs
            const qtyInputs = document.querySelectorAll('input[type="number"]');
            qtyInputs.forEach(input => {
                input.addEventListener('input', calculateTotals);
            });
            
            document.getElementById('other-amount').addEventListener('input', calculateTotals);
            
            // Print button
            document.getElementById('print-btn').addEventListener('click', function() {
                window.print();
            });
            
            // Download PDF button
            document.getElementById('download-pdf-btn').addEventListener('click', function() {
                // Create a clone of the invoice content
                const invoiceContent = document.getElementById('invoice-content').cloneNode(true);
                
                // Remove the action buttons from the clone
                const actionButtons = invoiceContent.querySelector('.no-print');
                if (actionButtons) {
                    actionButtons.remove();
                }
                
                // Convert form inputs to text in the clone
                const inputs = invoiceContent.querySelectorAll('input');
                inputs.forEach(input => {
                    const span = document.createElement('span');
                    span.textContent = input.value;
                    span.style.padding = '0.5rem';
                    span.style.display = 'block';
                    input.parentNode.replaceChild(span, input);
                });
                
                // Generate filename based on client name and date
                const clientName = document.getElementById('clientName').value || 'LUMASONIX';
                const quoteDate = document.getElementById('quoteDate').value || today;
                const filename = `${clientName}_報價單_${quoteDate}.pdf`;
                
                // PDF options
                const opt = {
                    margin: 10,
                    filename: filename,
                    image: { type: 'jpeg', quality: 0.98 },
                    html2canvas: { scale: 2 },
                    jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
                };
                
                // Generate PDF
                html2pdf().from(invoiceContent).set(opt).save();
            });
            
            // Reset button
            document.getElementById('reset-btn').addEventListener('click', function() {
                const qtyInputs = document.querySelectorAll('input[type="number"]');
                qtyInputs.forEach(input => {
                    input.value = 0;
                });
                
                document.getElementById('other-desc').value = '';
                document.getElementById('other-amount').value = 0;
                document.getElementById('clientName').value = '';
                document.getElementById('dispatchDate').value = '';
                document.getElementById('eventLocation').value = '';
                document.getElementById('contactPerson').value = '';
                document.getElementById('quoteNumber').value = '';
                document.getElementById('quoteDate').value = today;
                
                calculateTotals();
            });
            
            // Initial calculation
            calculateTotals();
        });
        
        function calculateTotals() {
            // Get quantities
            const staffQty = parseInt(document.getElementById('staff-qty').value) || 0;
            const controlQty = parseInt(document.getElementById('control-qty').value) || 0;
            const spotlightQty = parseInt(document.getElementById('spotlight-qty').value) || 0;
            const heightQty = parseInt(document.getElementById('height-qty').value) || 0;
            const overtimeQty = parseInt(document.getElementById('overtime-qty').value) || 0;
            const travelQty = parseInt(document.getElementById('travel-qty').value) || 0;
            const otherAmount = parseInt(document.getElementById('other-amount').value) || 0;
            
            // Calculate line totals
            const staffTotal = staffQty * 2500;
            const controlTotal = controlQty * 1000;
            const spotlightTotal = spotlightQty * 1000;
            const heightTotal = heightQty * 1000;
            const overtimeTotal = overtimeQty * 350;
            const travelTotal = travelQty * 300;
            const adminTotal = Math.round(staffTotal * 0.1);
            
            // Update line totals in the table
            document.getElementById('staff-total').textContent = formatCurrency(staffTotal);
            document.getElementById('control-total').textContent = formatCurrency(controlTotal);
            document.getElementById('spotlight-total').textContent = formatCurrency(spotlightTotal);
            document.getElementById('height-total').textContent = formatCurrency(heightTotal);
            document.getElementById('overtime-total').textContent = formatCurrency(overtimeTotal);
            document.getElementById('travel-total').textContent = formatCurrency(travelTotal);
            document.getElementById('admin-total').textContent = formatCurrency(adminTotal);
            
            // Calculate subtotal
            const subtotal = staffTotal + controlTotal + spotlightTotal + heightTotal + 
                            overtimeTotal + travelTotal + adminTotal + otherAmount;
            
            // Update subtotal and total
            document.getElementById('subtotal').textContent = 'NT$' + formatCurrency(subtotal);
            document.getElementById('total').textContent = 'NT$' + formatCurrency(subtotal);
        }
        
        function formatCurrency(amount) {
            return amount.toLocaleString('en-US');
        }
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'93e564f6a020f083',t:'MTc0NzAwNTQ5NS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
