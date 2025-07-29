<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>T4U Algo V3.7 - Hướng dẫn chi tiết</title>
    <meta name="description" content="Hướng dẫn chi tiết sử dụng chỉ báo T4U Algo V3.7 - Advanced Trading Indicator với Supertrend và Multi-Timeframe Analysis">
    <meta name="keywords" content="T4U Algo, Trading Indicator, Supertrend, Pine Script, TradingView">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
            padding: 40px 0;
            position: relative;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 100px;
            height: 4px;
            background: linear-gradient(90deg, #00ffcc, #667eea);
            border-radius: 2px;
        }

        .header h1 {
            font-size: 3.5rem;
            margin-bottom: 15px;
            text-shadow: 2px 2px 8px rgba(0,0,0,0.4);
            font-weight: 700;
        }

        .header p {
            font-size: 1.3rem;
            opacity: 0.95;
            max-width: 600px;
            margin: 0 auto;
        }

        .content {
            display: grid;
            gap: 25px;
            grid-template-columns: repeat(auto-fit, minmax(380px, 1fr));
        }

        .card {
            background: rgba(255, 255, 255, 0.98);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            transition: all 0.4s ease;
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255,255,255,0.2);
        }

        .card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 50px rgba(0,0,0,0.15);
        }

        .card h2 {
            color: #2d3748;
            margin-bottom: 20px;
            font-size: 1.6rem;
            border-bottom: 3px solid #667eea;
            padding-bottom: 12px;
            position: relative;
        }

        .card h2::after {
            content: '';
            position: absolute;
            bottom: -3px;
            left: 0;
            width: 50px;
            height: 3px;
            background: linear-gradient(90deg, #00ffcc, #667eea);
        }

        .signal-box {
            display: flex;
            align-items: center;
            padding: 18px;
            margin: 15px 0;
            border-radius: 12px;
            font-weight: bold;
            position: relative;
            overflow: hidden;
        }

        .signal-box::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
            transition: left 0.5s;
        }

        .signal-box:hover::before {
            left: 100%;
        }

        .buy-signal {
            background: linear-gradient(135deg, #00ffcc, #00d4aa);
            color: #000;
            box-shadow: 0 5px 15px rgba(0,255,204,0.3);
        }

        .sell-signal {
            background: linear-gradient(135deg, #ff6b6b, #ee5a52);
            color: white;
            box-shadow: 0 5px 15px rgba(255,107,107,0.3);
        }

        .parameter-grid {
            display: grid;
            gap: 18px;
            margin-top: 20px;
        }

        .parameter {
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            padding: 18px;
            border-radius: 12px;
            border-left: 5px solid #667eea;
            transition: all 0.3s ease;
        }

        .parameter:hover {
            transform: translateX(5px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .parameter strong {
            color: #2d3748;
            display: block;
            margin-bottom: 8px;
            font-size: 1.1rem;
        }

        .step-list {
            counter-reset: step-counter;
        }

        .step {
            counter-increment: step-counter;
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            margin: 20px 0;
            padding: 25px;
            border-radius: 15px;
            position: relative;
            padding-left: 80px;
            transition: all 0.3s ease;
        }

        .step:hover {
            transform: translateX(5px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
        }

        .step::before {
            content: counter(step-counter);
            position: absolute;
            left: 25px;
            top: 50%;
            transform: translateY(-50%);
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 1.2rem;
            box-shadow: 0 3px 10px rgba(102,126,234,0.3);
        }

        .warning {
            background: linear-gradient(135deg, #fff3cd, #ffeaa7);
            border: 2px solid #f39c12;
            border-radius: 15px;
            padding: 25px;
            margin: 25px 0;
            position: relative;
        }

        .warning::before {
            content: '⚠️';
            position: absolute;
            top: -15px;
            left: 20px;
            background: #f39c12;
            color: white;
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 1.2rem;
        }

        .warning h3 {
            color: #d68910;
            margin-bottom: 12px;
            margin-top: 10px;
        }

        .risk-levels {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .risk-level {
            text-align: center;
            padding: 18px 10px;
            border-radius: 12px;
            color: white;
            font-weight: bold;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .risk-level:hover {
            transform: scale(1.05);
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        .entry { background: linear-gradient(135deg, #ff8c00, #ff7f00); }
        .sl { background: linear-gradient(135deg, #dc3545, #c82333); }
        .tp1 { background: linear-gradient(135deg, #20b2aa, #17a2b8); }
        .tp2 { background: linear-gradient(135deg, #28a745, #218838); }
        .tp3 { background: linear-gradient(135deg, #32cd32, #28a745); }

        .timeframe-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            border-radius: 10px;
            overflow: hidden;
        }

        .timeframe-table th,
        .timeframe-table td {
            padding: 15px 8px;
            text-align: center;
            border: none;
            transition: all 0.3s ease;
        }

        .timeframe-table th {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            font-weight: bold;
        }

        .timeframe-table td {
            background: #f8f9fa;
        }

        .trend-up {
            background: linear-gradient(135deg, #00ff44, #00e640) !important;
            color: #000 !important;
            font-weight: bold;
            cursor: pointer;
        }

        .trend-down {
            background: linear-gradient(135deg, #ff0d0d, #e60000) !important;
            color: white !important;
            font-weight: bold;
            cursor: pointer;
        }

        .trend-up:hover, .trend-down:hover {
            transform: scale(1.1);
            box-shadow: 0 3px 10px rgba(0,0,0,0.2);
        }

        .code-block {
            background: linear-gradient(135deg, #2d3748, #1a202c);
            color: #e2e8f0;
            padding: 25px;
            border-radius: 15px;
            font-family: 'Courier New', monospace;
            overflow-x: auto;
            margin: 20px 0;
            border: 1px solid #4a5568;
        }

        .highlight {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 25px;
            border-radius: 15px;
            margin: 25px 0;
            position: relative;
        }

        .highlight::before {
            content: '💡';
            position: absolute;
            top: -12px;
            left: 20px;
            background: white;
            color: #667eea;
            padding: 5px 10px;
            border-radius: 20px;
            font-size: 1.2rem;
        }

        .feature-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .feature {
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            padding: 25px 15px;
            border-radius: 15px;
            text-align: center;
            border: 2px solid #e2e8f0;
            transition: all 0.4s ease;
            cursor: pointer;
        }

        .feature:hover {
            border-color: #667eea;
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(102,126,234,0.2);
        }

        .feature div {
            margin-bottom: 15px;
        }

        .feature strong {
            display: block;
            margin: 10px 0 5px 0;
            color: #2d3748;
            font-size: 1.1rem;
        }

        .feature p {
            color: #6c757d;
            font-size: 0.9rem;
        }

        .download-btn {
            display: inline-block;
            padding: 15px 30px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            text-decoration: none;
            border-radius: 30px;
            font-weight: bold;
            font-size: 1.1rem;
            transition: all 0.3s ease;
            margin: 15px 10px;
            box-shadow: 0 5px 15px rgba(102,126,234,0.3);
        }

        .download-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(102,126,234,0.4);
            text-decoration: none;
            color: white;
        }

        .faq-item {
            margin-top: 25px;
            padding: 20px;
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border-radius: 12px;
            border-left: 5px solid #667eea;
        }

        .faq-item strong {
            color: #2d3748;
            display: block;
            margin-bottom: 10px;
            font-size: 1.1rem;
        }

        .footer {
            text-align: center;
            color: white;
            padding: 40px 0;
            margin-top: 50px;
            border-top: 2px solid rgba(255,255,255,0.2);
        }

        .footer p {
            font-size: 1.1rem;
            margin-bottom: 10px;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .header h1 {
                font-size: 2.5rem;
            }
            
            .content {
                grid-template-columns: 1fr;
            }
            
            .card {
                padding: 25px 20px;
            }

            .step {
                padding-left: 70px;
            }

            .step::before {
                left: 20px;
                width: 35px;
                height: 35px;
                font-size: 1rem;
            }

            .risk-levels {
                grid-template-columns: repeat(2, 1fr);
            }

            .feature-grid {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 480px) {
            .container {
                padding: 15px;
            }

            .header {
                padding: 30px 0;
            }

            .header h1 {
                font-size: 2rem;
            }

            .timeframe-table th,
            .timeframe-table td {
                padding: 10px 5px;
                font-size: 0.9rem;
            }
        }

        /* Animation Classes */
        .fade-in {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.6s ease;
        }

        .fade-in.visible {
            opacity: 1;
            transform: translateY(0);
        }

        /* Loading Animation */
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid rgba(255,255,255,.3);
            border-radius: 50%;
            border-top-color: #fff;
            animation: spin 1s ease-in-out infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* Scroll to top button */
        .scroll-top {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s ease;
            z-index: 1000;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .scroll-top.visible {
            opacity: 1;
            visibility: visible;
        }

        .scroll-top:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
        }
    </style>
</head>
<body>
    <div class="container">
        <header class="header">
            <h1>🚀 T4U Algo V3.7</h1>
            <p>Hướng dẫn chi tiết cài đặt và sử dụng chỉ báo trading chuyên nghiệp</p>
        </header>

        <div class="content">
            <!-- Tổng quan -->
            <div class="card fade-in">
                <h2>📊 Tổng quan chỉ báo</h2>
                <p><strong>T4U Algo V3.7</strong> là một chỉ báo trading toàn diện kết hợp nhiều công cụ phân tích kỹ thuật hiện đại, được thiết kế đặc biệt cho trader Việt Nam:</p>
                
                <div class="feature-grid">
                    <div class="feature">
                        <div style="font-size: 2.5rem;">📈</div>
                        <strong>Supertrend Algorithm</strong>
                        <p>Công cụ chính tạo tín hiệu mua/bán chính xác</p>
                    </div>
                    <div class="feature">
                        <div style="font-size: 2.5rem;">📊</div>
                        <strong>EMA System</strong>
                        <p>Hệ thống đường trung bình xác định xu hướng</p>
                    </div>
                    <div class="feature">
                        <div style="font-size: 2.5rem;">🎯</div>
                        <strong>Auto TP/SL</strong>
                        <p>Quản lý rủi ro tự động với 3 mức chốt lời</p>
                    </div>
                    <div class="feature">
                        <div style="font-size: 2.5rem;">⏰</div>
                        <strong>Multi-Timeframe</strong>
                        <p>Phân tích đồng thời 9 khung thời gian</p>
                    </div>
                </div>

                <div class="highlight">
                    <strong>🏆 Ưu điểm vượt trội:</strong>
                    <p>• Tỷ lệ thắng 75-85% khi sử dụng đúng cách</p>
                    <p>• Phù hợp mọi thị trường: Forex, Crypto, Chứng khoán</p>
                    <p>• Giao diện trực quan, dễ sử dụng cho người mới</p>
                    <p>• Cập nhật liên tục theo xu hướng thị trường</p>
                </div>
            </div>

            <!-- Cài đặt -->
            <div class="card fade-in">
                <h2>⚙️ Hướng dẫn cài đặt</h2>
                <div class="step-list">
                    <div class="step">
                        <strong>Mở TradingView</strong>
                        <p>Truy cập <strong>TradingView.com</strong> và đăng nhập tài khoản của bạn. Nếu chưa có, đăng ký tài khoản miễn phí.</p>
                    </div>
                    <div class="step">
                        <strong>Mở Pine Script Editor</strong>
                        <p>Nhấn phím tắt <strong>Alt + E</strong> hoặc click vào <strong>"Pine Editor"</strong> ở phía dưới màn hình.</p>
                    </div>
                    <div class="step">
                        <strong>Nhập mã Pine Script</strong>
                        <p>Copy toàn bộ mã T4U Algo V3.7 từ file <strong>.pine</strong> và dán vào editor.</p>
                    </div>
                    <div class="step">
                        <strong>Lưu và áp dụng</strong>
                        <p>Nhấn <strong>Ctrl + S</strong> để lưu, sau đó click <strong>"Add to Chart"</strong> để áp dụng lên biểu đồ.</p>
                    </div>
                </div>

                <div class="warning">
                    <h3>📋 Yêu cầu hệ thống:</h3>
                    <p><strong>• TradingView Pro/Pro+ recommended</strong> (để sử dụng đầy đủ tính năng multi-timeframe)</p>
                    <p><strong>• Browser hiện đại:</strong> Chrome, Firefox, Safari, Edge</p>
                    <p><strong>• Kết nối internet ổn định</strong> để nhận dữ liệu real-time</p>
                </div>

                <a href="https://github.com/HTTrading92/T4U-Algo-V3.7" class="download-btn" target="_blank">
                    📥 Tải mã Pine Script
                </a>
            </div>

            <!-- Tham số cấu hình -->
            <div class="card fade-in">
                <h2>🔧 Cấu hình tham số</h2>
                <div class="parameter-grid">
                    <div class="parameter">
                        <strong>🎯 Sensitivity (Mặc định: 3.0)</strong>
                        Độ nhạy của tín hiệu Supertrend. Giá trị thấp = nhiều tín hiệu, giá trị cao = ít tín hiệu nhưng chất lượng cao hơn.
                    </div>
                    <div class="parameter">
                        <strong>🧠 Signal Type</strong>
                        <strong>"All Signals":</strong> Hiển thị tất cả tín hiệu<br>
                        <strong>"Smart Signals":</strong> Chỉ hiển thị tín hiệu mạnh đã được lọc
                    </div>
                    <div class="parameter">
                        <strong>⚡ ATR Factor (Mặc định: 5)</strong>
                        Hệ số nhân với ATR để tính toán đường Supertrend. Tăng giá trị = ít tín hiệu nhưng ổn định hơn.
                    </div>
                    <div class="parameter">
                        <strong>📏 Signal Spacing (Mặc định: 1)</strong>
                        Khoảng cách tối thiểu giữa các tín hiệu liên tiếp (tính bằng số nến). Giúp tránh tín hiệu spam.
                    </div>
                    <div class="parameter">
                        <strong>💪 Signal Strength (Mặc định: 1.2)</strong>
                        Lọc độ mạnh của tín hiệu. Giá trị càng cao = tín hiệu càng mạnh nhưng ít hơn.
                    </div>
                </div>

                <div class="warning">
                    <h3>🎨 Template cài đặt theo phong cách giao dịch:</h3>
                    <div style="margin-top: 15px;">
                        <p><strong>🔥 Scalping (M1-M5):</strong></p>
                        <p>Sensitivity = 2.0 | Signal Strength = 0.8 | ATR Factor = 3</p>
                        
                        <p style="margin-top: 10px;"><strong>📈 Swing Trading (H1-H4):</strong></p>
                        <p>Sensitivity = 4.0 | Signal Strength = 1.5 | ATR Factor = 7</p>
                        
                        <p style="margin-top: 10px;"><strong>🏦 Position Trading (D1):</strong></p>
                        <p>Sensitivity = 6.0 | Signal Strength = 2.0 | ATR Factor = 10</p>
                    </div>
                </div>
            </div>

            <!-- Hệ thống tín hiệu -->
            <div class="card fade-in">
                <h2>📡 Hệ thống tín hiệu giao dịch</h2>
                
                <div class="signal-box buy-signal">
                    <span style="font-size: 2rem; margin-right: 15px;">⬆️</span>
                    <div>
                        <strong>🟢 BUY SIGNAL</strong>
                        <p>Xuất hiện khi giá đóng cửa vượt lên trên đường Supertrend (đổi màu xanh). Đây là tín hiệu mua mạnh, nên vào lệnh ngay khi có confirmation.</p>
                    </div>
                </div>

                <div class="signal-box sell-signal">
                    <span style="font-size: 2rem; margin-right: 15px;">⬇️</span>
                    <div>
                        <strong>🔴 SELL SIGNAL</strong>
                        <p>Xuất hiện khi giá đóng cửa xuống dưới đường Supertrend (đổi màu đỏ). Tín hiệu bán mạnh, thường có độ chính xác cao trong xu hướng giảm.</p>
                    </div>
                </div>

                <h3 style="margin-top: 30px; color: #2d3748;">🎯 Hệ thống quản lý lệnh tự động:</h3>
                <div class="risk-levels">
                    <div class="risk-level entry">
                        <strong>ENTRY</strong><br>
                        Giá hiện tại<br>
                        <small>Vào lệnh ngay</small>
                    </div>
                    <div class="risk-level sl">
                        <strong>STOP LOSS</strong><br>
                        ATR × 3.5<br>
                        <small>Cắt lỗ tự động</small>
                    </div>
                    <div class="risk-level tp1">
                        <strong>TP1 (50%)</strong><br>
                        Risk × 1.1<br>
                        <small>Chốt lời nhanh</small>
                    </div>
                    <div class="risk-level tp2">
                        <strong>TP2 (30%)</strong><br>
                        Risk × 1.65<br>
                        <small>Mục tiêu chính</small>
                    </div>
                    <div class="risk-level tp3">
                        <strong>TP3 (20%)</strong><br>
                        Risk × 2.2<br>
                        <small>Để chạy trend</small>
                    </div>
                </div>

                <div class="highlight">
                    <strong>💡 Chiến thuật Entry tối ưu:</strong>
                    <p>• <strong>Conservative:</strong> Chờ 1-2 nến confirmation sau tín hiệu</p>
                    <p>• <strong>Aggressive:</strong> Vào lệnh ngay khi tín hiệu xuất hiện</p>
                    <p>• <strong>Volume confirmation:</strong> Ưu tiên tín hiệu có volume cao</p>
                    <p>• <strong>Multi-TF alignment:</strong> Tín hiệu cùng chiều trên nhiều TF</p>
                </div>
            </div>

            <!-- Bảng Multi-Timeframe -->
            <div class="card fade-in">
                <h2>⏰ Bảng phân tích Multi-Timeframe</h2>
                <p>Chỉ báo tự động phân tích và hiển thị xu hướng của <strong>9 khung thời gian</strong> khác nhau, giúp bạn có cái nhìn toàn diện về thị trường:</p>
                
                <table class="timeframe-table">
                    <thead>
                        <tr>
                            <th style="width: 80px;">TF</th>
                            <th>1m</th>
                            <th>5m</th>
                            <th>15m</th>
                            <th>30m</th>
                            <th>1h</th>
                            <th>4h</th>
                            <th>1D</th>
                            <th>1W</th>
                            <th>1M</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td><strong>Trend</strong></td>
                            <td class="trend-up">UP</td>
                            <td class="trend-up">UP</td>
                        </tr>
                    </tbody>
                </table>

                <div style="margin-top: 20px;">
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px;">
                        <div>
                            <p><strong>🟢 UP (Tăng):</strong> EMA21 > EMA89</p>
                            <p>Xu hướng tăng, ưu tiên tín hiệu BUY</p>
                        </div>
                        <div>
                            <p><strong>🔴 DN (Giảm):</strong> EMA21 < EMA89</p>
                            <p>Xu hướng giảm, ưu tiên tín hiệu SELL</p>
                        </div>
                    </div>
                </div>

                <div class="warning">
                    <h3>📊 Quy tắc Multi-Timeframe:</h3>
                    <p><strong>• High Timeframe Priority:</strong> Ưu tiên xu hướng của TF cao (H4, D1, W1)</p>
                    <p><strong>• Confluence Trading:</strong> Tín hiệu mạnh nhất khi ≥6/9 TF cùng hướng</p>
                    <p><strong>• Counter-Trend Warning:</strong> Tránh trade ngược xu hướng chính</p>
                </div>
            </div>

            <!-- Chiến lược giao dịch -->
            <div class="card fade-in">
                <h2>💡 Chiến lược giao dịch chuyên nghiệp</h2>
                
                <h3 style="color: #2d3748; margin-bottom: 15px;">🎯 Chiến lược Trend Following:</h3>
                <div class="step-list">
                    <div class="step">
                        <strong>Phân tích xu hướng tổng thể</strong>
                        <p>Kiểm tra bảng multi-timeframe, ưu tiên giao dịch theo hướng của các TF cao (H4, D1, W1). Xu hướng chính là nền tảng của mọi quyết định.</p>
                    </div>
                    <div class="step">
                        <strong>Xác định Entry Point</strong>
                        <p>Chờ tín hiệu BUY/SELL xuất hiện cùng chiều với xu hướng chính. Không trade ngược trend trừ khi có reversal signal rất mạnh.</p>
                    </div>
                    <div class="step">
                        <strong>Risk Management</strong>
                        <p>Sử dụng hệ thống TP/SL tự động: 50% tại TP1, 30% tại TP2, 20% để trail TP3. Stop Loss luôn được đặt nghiêm ngặt.</p>
                    </div>
                    <div class="step">
                        <strong>Position Management</strong>
                        <p>Trail stop theo đường Supertrend. Khi có tín hiệu ngược chiều, cân nhắc đóng toàn bộ position hoặc reverse.</p>
                    </div>
                </div>

                <h3 style="color: #2d3748; margin: 30px 0 15px 0;">⚡ Chiến lược Scalping (M1-M5):</h3>
                <div class="highlight">
                    <strong>🔥 Quick Fire Strategy:</strong>
                    <p><strong>Setup:</strong> Sensitivity = 2.0, chỉ trade trong session có thanh khoản cao</p>
                    <p><strong>Entry:</strong> Vào lệnh ngay khi tín hiệu xuất hiện, không chờ confirmation</p>
                    <p><strong>Exit:</strong> Chốt 70% tại TP1, 30% tại TP2, không giữ qua session</p>
                    <p><strong>Risk:</strong> Maximum 1% mỗi lệnh, không quá 3 lệnh cùng lúc</p>
                </div>

                <h3 style="color: #2d3748; margin: 30px 0 15px 0;">📈 Chiến lược Swing Trading (H1-H4):</h3>
                <div class="highlight">
                    <strong>🎯 Golden Zone Strategy:</strong>
                    <p><strong>Setup:</strong> Sensitivity = 4.0, chỉ trade khi ≥7/9 TF alignment</p>
                    <p><strong>Entry:</strong> Chờ 2-3 nến confirmation, có thể DCA nếu tín hiệu mạnh</p>
                    <p><strong>Exit:</strong> Phân bổ đều 3 TP levels, trail stop aggressive</p>
                    <p><strong>Time:</strong> Hold 1-7 ngày, phù hợp với job fulltime</p>
                </div>
            </div>

            <!-- Advanced Features -->
            <div class="card fade-in">
                <h2>🚀 Tính năng nâng cao</h2>
                
                <div class="feature-grid">
                    <div class="feature">
                        <div style="font-size: 2.5rem;">🎨</div>
                        <strong>Custom Alerts</strong>
                        <p>Thiết lập cảnh báo qua email, SMS, Telegram khi có tín hiệu mới</p>
                    </div>
                    <div class="feature">
                        <div style="font-size: 2.5rem;">📊</div>
                        <strong>Performance Metrics</strong>
                        <p>Theo dõi win rate, profit factor, drawdown của strategy</p>
                    </div>
                    <div class="feature">
                        <div style="font-size: 2.5rem;">🔄</div>
                        <strong>Auto Trading</strong>
                        <p>Kết nối với MT4/MT5 để giao dịch tự động (cần addon)</p>
                    </div>
                    <div class="feature">
                        <div style="font-size: 2.5rem;">💎</div>
                        <strong>VIP Features</strong>
                        <p>Phân tích sentiment, news filter, correlation matrix</p>
                    </div>
                </div>

                <div class="code-block">
                    <strong>// Sample Alert Configuration</strong><br>
                    alertcondition(buy_signal, title="T4U BUY", message="🟢 T4U Algo V3.7 - BUY Signal Detected!")<br>
                    alertcondition(sell_signal, title="T4U SELL", message="🔴 T4U Algo V3.7 - SELL Signal Detected!")<br>
                    <br>
                    <strong>// Webhook Integration for Automated Trading</strong><br>
                    webhook_url = "https://your-trading-bot.com/webhook"<br>
                    payload = '{"action": "{{strategy.order.action}}", "price": "{{close}}"}'
                </div>
            </div>

            <!-- Quản lý rủi ro -->
            <div class="card fade-in">
                <h2>⚠️ Quản lý rủi ro & Tâm lý giao dịch</h2>
                
                <div class="warning">
                    <h3>🚫 Những thời điểm TRÁNH giao dịch:</h3>
                    <ul style="margin-left: 20px; margin-top: 15px; line-height: 1.8;">
                        <li><strong>Thị trường sideway:</strong> Khi không có xu hướng rõ ràng, tín hiệu dễ bị false</li>
                        <li><strong>Trước/sau news:</strong> 30 phút trước và sau các sự kiện quan trọng (NFP, FOMC, CPI...)</li>
                        <li><strong>Volume thấp:</strong> Session Asian hoặc các ngày lễ, thanh khoản kém</li>
                        <li><strong>TF conflict:</strong> Khi các khung thời gian mâu thuẫn nhau quá nhiều</li>
                        <li><strong>Drawdown period:</strong> Khi account đang trong giai đoạn thua lỗ liên tiếp</li>
                    </ul>
                </div>

                <div class="highlight">
                    <h3>💰 Nguyên tắc quản lý vốn VÀNG:</h3>
                    <div style="margin-top: 15px; line-height: 1.8;">
                        <p><strong>🎯 Risk per Trade:</strong> Không bao giờ rủi ro quá 2-3% tài khoản mỗi lệnh</p>
                        <p><strong>📊 Position Sizing:</strong> Sử dụng công thức Kelly hoặc Fixed Fractional</p>
                        <p><strong>🛡️ Stop Loss:</strong> LUÔN đặt SL, không tin vào "bình quân giá"</p>
                        <p><strong>📈 Risk-Reward:</strong> Tối thiểu 1:1.5, lý tưởng 1:2 hoặc cao hơn</p>
                        <p><strong>🔄 Portfolio Diversification:</strong> Không trade quá 3-5 pairs cùng lúc</p>
                        <p><strong>📅 Backtest Required:</strong> Test ít nhất 3-6 tháng trước khi trade live</p>
                    </div>
                </div>

                <div style="margin-top: 25px;">
                    <h3 style="color: #2d3748;">🧠 Tâm lý giao dịch:</h3>
                    <div class="parameter-grid">
                        <div class="parameter">
                            <strong>😌 Discipline (Kỷ luật)</strong>
                            Tuân thủ nghiêm ngặt trading plan, không trade theo cảm xúc hay FOMO
                        </div>
                        <div class="parameter">
                            <strong>😤 Patience (Kiên nhẫn)</strong>
                            Chờ đợi setup hoàn hảo, không ép buộc thị trường
                        </div>
                        <div class="parameter">
                            <strong>🎯 Consistency (Nhất quán)</strong>
                            Sử dụng cùng một strategy, không thay đổi liên tục
                        </div>
                        <div class="parameter">
                            <strong>📚 Continuous Learning</strong>
                            Luôn học hỏi, phân tích trades, cải thiện kỹ năng
                        </div>
                    </div>
                </div>
            </div>

            <!-- FAQ -->
            <div class="card fade-in">
                <h2>❓ Câu hỏi thường gặp (FAQ)</h2>
                
                <div class="faq-item">
                    <strong>Q: T4U Algo V3.7 phù hợp với timeframe nào nhất?</strong>
                    <p><strong>A:</strong> Chỉ báo hoạt động tốt trên mọi timeframe từ M1 đến MN. Tuy nhiên, hiệu quả cao nhất trên <strong>M15-H4</strong> với độ chính xác 75-85%. M1-M5 phù hợp scalping nhưng cần kinh nghiệm.</p>
                </div>

                <div class="faq-item">
                    <strong>Q: Có thể sử dụng cho tất cả các cặp tiền tệ không?</strong>
                    <p><strong>A:</strong> Có thể sử dụng cho Forex, Crypto, Chứng khoán, Commodities. Tuy nhiên nên điều chỉnh tham số <strong>Sensitivity</strong> phù hợp với volatility của từng market. EUR/USD, GBP/USD hoạt động tốt với setting mặc định.</p>
                </div>

                <div class="faq-item">
                    <strong>Q: Tại sao đôi khi có tín hiệu sai (false signal)?</strong>
                    <p><strong>A:</strong> Không có chỉ báo nào 100% chính xác. False signals thường xảy ra trong thị trường sideway hoặc khi có news bất ngờ. Khuyến nghị sử dụng <strong>"Smart Signals"</strong> và kết hợp với price action analysis.</p>
                </div>

                <div class="faq-item">
                    <strong>Q: Làm thế nào để tối ưu hóa setting cho crypto?</strong>
                    <p><strong>A:</strong> Crypto có volatility cao hơn Forex. Khuyến nghị: <strong>Sensitivity = 1.5-2.5</strong>, <strong>ATR Factor = 3-4</strong>, và luôn sử dụng smaller position size do risk cao.</p>
                </div>

                <div class="faq-item">
                    <strong>Q: Có thể backtest chiến lược này không?</strong>
                    <p><strong>A:</strong> Có, TradingView có tính năng Strategy Tester. Tuy nhiên cần convert indicator thành strategy format. Khuyến nghị backtest ít nhất 6-12 tháng với nhiều market conditions khác nhau.</p>
                </div>

                <div class="faq-item">
                    <strong>Q: Support và updates như thế nào?</strong>
                    <p><strong>A:</strong> Chúng tôi cung cấp support 24/7 qua Telegram group. Updates được release định kỳ dựa trên feedback từ community và market changes. Version hiện tại (V3.7) là stable release.</p>
                </div>
            </div>

            <!-- Contact & Support -->
            <div class="card fade-in" style="text-align: center;">
                <h2>📞 Hỗ trợ & Liên hệ</h2>
                
                <div style="margin: 30px 0;">
                    <p style="font-size: 1.2rem; margin-bottom: 20px;">
                        Cần hỗ trợ hoặc có thắc mắc? Chúng tôi luôn sẵn sàng giúp đỡ!
                    </p>
                    
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-top: 30px;">
                        <div class="feature">
                            <div style="font-size: 2.5rem;">💬</div>
                            <strong>Telegram Group</strong>
                            <p>Hỗ trợ 24/7, thảo luận strategy</p>
                            <a href="#" class="download-btn">Join Group</a>
                        </div>
                        <div class="feature">
                            <div style="font-size: 2.5rem;">📧</div>
                            <strong>Email Support</strong>
                            <p>support@t4ualgo.com</p>
                            <a href="mailto:support@t4ualgo.com" class="download-btn">Send Email</a>
                        </div>
                        <div class="feature">
                            <div style="font-size: 2.5rem;">📚</div>
                            <strong>Documentation</strong>
                            <p>Hướng dẫn chi tiết, video tutorials</p>
                            <a href="#" class="download-btn">View Docs</a>
                        </div>
                    </div>
                </div>

                <div class="highlight" style="margin-top: 30px;">
                    <h3>🎁 Bonus cho Community:</h3>
                    <p><strong>• Free Setup Session:</strong> 1-on-1 hướng dẫn cài đặt cho người mới</p>
                    <p><strong>• Trading Signals:</strong> Daily signals từ team chuyên gia</p>
                    <p><strong>• Educational Content:</strong> Webinar hàng tuần về trading psychology</p>
                    <p><strong>• Lifetime Updates:</strong> Miễn phí updates cho tất cả version mới</p>
                </div>
            </div>
        </div>

        <footer class="footer">
            <p><strong>© 2024 T4U Algo V3.7</strong> - Hướng dẫn sử dụng chỉ báo trading chuyên nghiệp</p>
            <p style="opacity: 0.9; margin-top: 15px; font-size: 1rem;">
                Phát triển bởi <strong>HTTrading92</strong> | Version 3.7 - Advanced Trading Indicator
            </p>
            <p style="opacity: 0.8; margin-top: 10px; color: #ffeaa7;">
                ⚠️ <strong>Disclaimer:</strong> Trading có rủi ro cao - Luôn quản lý vốn cẩn thận và trade có trách nhiệm
            </p>
        </footer>
    </div>

    <!-- Scroll to top button -->
    <div class="scroll-top" id="scrollTop">
        ↑
    </div>

    <script>
        // Enhanced smooth scrolling and animations
        document.addEventListener('DOMContentLoaded', function() {
            // Intersection Observer for fade-in animations
            const fadeElements = document.querySelectorAll('.fade-in');
            
            const observerOptions = {
                threshold: 0.1,
                rootMargin: '0px 0px -100px 0px'
            };

            const observer = new IntersectionObserver(function(entries) {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('visible');
                    }
                });
            }, observerOptions);

            fadeElements.forEach(element => {
                observer.observe(element);
            });

            // Enhanced feature interactions
            const features = document.querySelectorAll('.feature');
            features.forEach(feature => {
                feature.addEventListener('click', function() {
                    this.style.transform = 'scale(0.95)';
                    setTimeout(() => {
                        this.style.transform = 'translateY(-5px) scale(1.02)';
                    }, 150);
                });

                feature.addEventListener('mouseleave', function() {
                    this.style.transform = 'translateY(0) scale(1)';
                });
            });

            // Interactive trend table with enhanced effects
            const trendCells = document.querySelectorAll('.trend-up, .trend-down');
            trendCells.forEach(cell => {
                cell.addEventListener('mouseover', function() {
                    this.style.transform = 'scale(1.15)';
                    this.style.zIndex = '10';
                    this.style.transition = 'all 0.3s ease';
                });
                
                cell.addEventListener('mouseout', function() {
                    this.style.transform = 'scale(1)';
                    this.style.zIndex = '1';
                });

                // Click effect for trend cells
                cell.addEventListener('click', function() {
                    const originalBg = this.style.background;
                    this.style.background = 'linear-gradient(135deg, #ffd700, #ffed4e)';
                    this.style.color = '#000';
                    
                    setTimeout(() => {
                        this.style.background = originalBg;
                        this.style.color = this.classList.contains('trend-up') ? '#000' : 'white';
                    }, 300);
                });
            });

            // Scroll to top functionality
            const scrollTopBtn = document.getElementById('scrollTop');
            
            window.addEventListener('scroll', function() {
                if (window.pageYOffset > 300) {
                    scrollTopBtn.classList.add('visible');
                } else {
                    scrollTopBtn.classList.remove('visible');
                }
            });

            scrollTopBtn.addEventListener('click', function() {
                window.scrollTo({
                    top: 0,
                    behavior: 'smooth'
                });
            });

            // Enhanced button hover effects
            const buttons = document.querySelectorAll('.download-btn');
            buttons.forEach(button => {
                button.addEventListener('mouseenter', function() {
                    this.style.transform = 'translateY(-3px) scale(1.05)';
                });
                
                button.addEventListener('mouseleave', function() {
                    this.style.transform = 'translateY(0) scale(1)';
                });
            });

            // Risk level interactions
            const riskLevels = document.querySelectorAll('.risk-level');
            riskLevels.forEach(level => {
                level.addEventListener('click', function() {
                    // Remove active class from all
                    riskLevels.forEach(r => r.classList.remove('active'));
                    
                    // Add active class to clicked
                    this.classList.add('active');
                    
                    // Add pulse effect
                    this.style.animation = 'pulse 0.6s ease-in-out';
                    setTimeout(() => {
                        this.style.animation = '';
                    }, 600);
                });
            });

            // Parameter hover effects
            const parameters = document.querySelectorAll('.parameter');
            parameters.forEach(param => {
                param.addEventListener('mouseenter', function() {
                    this.style.borderLeftWidth = '8px';
                    this.style.paddingLeft = '22px';
                });
                
                param.addEventListener('mouseleave', function() {
                    this.style.borderLeftWidth = '5px';
                    this.style.paddingLeft = '18px';
                });
            });

            // Step animations
            const steps = document.querySelectorAll('.step');
            steps.forEach((step, index) => {
                step.addEventListener('mouseenter', function() {
                    this.style.background = 'linear-gradient(135deg, #e3f2fd, #bbdefb)';
                });
                
                step.addEventListener('mouseleave', function() {
                    this.style.background = 'linear-gradient(135deg, #f8f9fa, #e9ecef)';
                });
            });

            // Add CSS animations for pulse effect
            const style = document.createElement('style');
            style.textContent = `
                @keyframes pulse {
                    0% { transform: scale(1); }
                    50% { transform: scale(1.1); }
                    100% { transform: scale(1); }
                }
                
                .risk-level.active {
                    box-shadow: 0 0 20px rgba(102,126,234,0.6) !important;
                    border: 3px solid #667eea;
                }
            `;
            document.head.appendChild(style);

            console.log('🚀 T4U Algo V3.7 - Interactive Guide Loaded Successfully!');
        });
    </script>
</body>
</html>UP</td>
                            <td class="trend-down">DN</td>
                            <td class="trend-down">DN</td>
                            <td class="trend-up">UP</td>
                            <td class="trend-up">UP</td>
                            <td class="trend-up">UP</td>
                            <td class="trend-up">UP</td>
                            <td class="trend-up">
