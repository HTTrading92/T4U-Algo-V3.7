<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>T4U Algo V3.7 - Hướng dẫn chi tiết</title>
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
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            color: white;
            margin-bottom: 30px;
            padding: 30px 0;
        }

        .header h1 {
            font-size: 3rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header p {
            font-size: 1.2rem;
            opacity: 0.9;
        }

        .content {
            display: grid;
            gap: 20px;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
        }

        .card {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            backdrop-filter: blur(10px);
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0,0,0,0.3);
        }

        .card h2 {
            color: #4a5568;
            margin-bottom: 15px;
            font-size: 1.5rem;
            border-bottom: 3px solid #667eea;
            padding-bottom: 10px;
        }

        .signal-box {
            display: flex;
            align-items: center;
            padding: 15px;
            margin: 10px 0;
            border-radius: 10px;
            font-weight: bold;
        }

        .buy-signal {
            background: linear-gradient(135deg, #00ffcc, #00e6b8);
            color: #000;
        }

        .sell-signal {
            background: linear-gradient(135deg, #e43a72, #d63384);
            color: white;
        }

        .parameter-grid {
            display: grid;
            gap: 15px;
            margin-top: 15px;
        }

        .parameter {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            border-left: 4px solid #667eea;
        }

        .parameter strong {
            color: #4a5568;
            display: block;
            margin-bottom: 5px;
        }

        .step-list {
            counter-reset: step-counter;
        }

        .step {
            counter-increment: step-counter;
            background: #f8f9fa;
            margin: 15px 0;
            padding: 20px;
            border-radius: 10px;
            position: relative;
            padding-left: 60px;
        }

        .step::before {
            content: counter(step-counter);
            position: absolute;
            left: 20px;
            top: 20px;
            background: #667eea;
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        .warning {
            background: linear-gradient(135deg, #ffecd1, #fcb045);
            border: 2px solid #f6ad55;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
        }

        .warning h3 {
            color: #c05621;
            margin-bottom: 10px;
        }

        .risk-levels {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .risk-level {
            text-align: center;
            padding: 15px;
            border-radius: 10px;
            color: white;
            font-weight: bold;
        }

        .entry { background: #ff8c00; }
        .sl { background: #dc3545; }
        .tp1 { background: #20b2aa; }
        .tp2 { background: #28a745; }
        .tp3 { background: #32cd32; }

        .timeframe-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
        }

        .timeframe-table th,
        .timeframe-table td {
            padding: 10px;
            text-align: center;
            border: 1px solid #ddd;
        }

        .timeframe-table th {
            background: #667eea;
            color: white;
        }

        .trend-up {
            background: #00ff44;
            color: #000;
            font-weight: bold;
        }

        .trend-down {
            background: #ff0d0d;
            color: white;
            font-weight: bold;
        }

        .code-block {
            background: #2d3748;
            color: #e2e8f0;
            padding: 20px;
            border-radius: 10px;
            font-family: 'Courier New', monospace;
            overflow-x: auto;
            margin: 15px 0;
        }

        .highlight {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
        }

        .feature-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .feature {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            text-align: center;
            border: 2px solid #e2e8f0;
            transition: all 0.3s ease;
        }

        .feature:hover {
            border-color: #667eea;
            transform: scale(1.02);
        }

        .feature i {
            font-size: 2rem;
            color: #667eea;
            margin-bottom: 10px;
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 2rem;
            }
            
            .content {
                grid-template-columns: 1fr;
            }
            
            .card {
                padding: 20px;
            }
        }

        .btn {
            display: inline-block;
            padding: 12px 24px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            text-decoration: none;
            border-radius: 25px;
            font-weight: bold;
            transition: all 0.3s ease;
            margin: 10px 5px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .footer {
            text-align: center;
            color: white;
            padding: 30px 0;
            margin-top: 40px;
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
            <div class="card">
                <h2>📊 Tổng quan chỉ báo</h2>
                <p><strong>T4U Algo V3.7</strong> là một chỉ báo trading toàn diện kết hợp nhiều công cụ phân tích kỹ thuật:</p>
                
                <div class="feature-grid">
                    <div class="feature">
                        <div style="font-size: 2rem;">📈</div>
                        <strong>Supertrend</strong>
                        <p>Công cụ chính tạo tín hiệu</p>
                    </div>
                    <div class="feature">
                        <div style="font-size: 2rem;">📊</div>
                        <strong>EMA System</strong>
                        <p>Xác định xu hướng</p>
                    </div>
                    <div class="feature">
                        <div style="font-size: 2rem;">🎯</div>
                        <strong>Auto TP/SL</strong>
                        <p>Quản lý rủi ro tự động</p>
                    </div>
                    <div class="feature">
                        <div style="font-size: 2rem;">⏰</div>
                        <strong>Multi-Timeframe</strong>
                        <p>Phân tích đa khung thời gian</p>
                    </div>
                </div>
            </div>

            <!-- Cài đặt -->
            <div class="card">
                <h2>⚙️ Cài đặt chỉ báo</h2>
                <div class="step-list">
                    <div class="step">
                        <strong>Mở TradingView</strong>
                        <p>Truy cập TradingView.com và đăng nhập tài khoản của bạn</p>
                    </div>
                    <div class="step">
                        <strong>Pine Script Editor</strong>
                        <p>Nhấn Alt+E hoặc vào Pine Editor ở phía dưới màn hình</p>
                    </div>
                    <div class="step">
                        <strong>Dán code</strong>
                        <p>Copy toàn bộ mã Pine Script và dán vào editor</p>
                    </div>
                    <div class="step">
                        <strong>Save & Add to Chart</strong>
                        <p>Nhấn Ctrl+S để lưu, sau đó "Add to Chart" để áp dụng</p>
                    </div>
                </div>

                <div class="highlight">
                    <strong>💡 Lưu ý:</strong> Cần tài khoản TradingView Pro+ để sử dụng đầy đủ tính năng multi-timeframe
                </div>
            </div>

            <!-- Tham số -->
            <div class="card">
                <h2>🔧 Cài đặt tham số</h2>
                <div class="parameter-grid">
                    <div class="parameter">
                        <strong>Sensitivity (3.0)</strong>
                        Độ nhạy của Supertrend. Giảm = nhiều tín hiệu, Tăng = ít tín hiệu
                    </div>
                    <div class="parameter">
                        <strong>Signal Type</strong>
                        "All Signals" = tất cả tín hiệu | "Smart Signals" = lọc tín hiệu mạnh
                    </div>
                    <div class="parameter">
                        <strong>Factor (5)</strong>
                        Hệ số tính toán ATR cho Supertrend
                    </div>
                    <div class="parameter">
                        <strong>Signal Spacing (1)</strong>
                        Khoảng cách tối thiểu giữa các tín hiệu (số nến)
                    </div>
                    <div class="parameter">
                        <strong>Signal Strength (1.2)</strong>
                        Lọc độ mạnh tín hiệu. Càng cao càng ít tín hiệu
                    </div>
                </div>

                <div class="warning">
                    <h3>⚠️ Khuyến nghị cài đặt</h3>
                    <p><strong>Scalping (M1-M5):</strong> Sensitivity = 2.0, Signal Strength = 0.8</p>
                    <p><strong>Swing Trading (H1-H4):</strong> Sensitivity = 4.0, Signal Strength = 1.5</p>
                    <p><strong>Position Trading (D1):</strong> Sensitivity = 6.0, Signal Strength = 2.0</p>
                </div>
            </div>

            <!-- Tín hiệu -->
            <div class="card">
                <h2>📡 Hệ thống tín hiệu</h2>
                
                <div class="signal-box buy-signal">
                    <span style="font-size: 1.5rem; margin-right: 10px;">⬆️</span>
                    <div>
                        <strong>BUY SIGNAL</strong>
                        <p>Khi giá đóng cửa vượt lên trên đường Supertrend (màu xanh)</p>
                    </div>
                </div>

                <div class="signal-box sell-signal">
                    <span style="font-size: 1.5rem; margin-right: 10px;">⬇️</span>
                    <div>
                        <strong>SELL SIGNAL</strong>
                        <p>Khi giá đóng cửa xuống dưới đường Supertrend (màu đỏ)</p>
                    </div>
                </div>

                <h3 style="margin-top: 20px;">🎯 Quản lý lệnh tự động:</h3>
                <div class="risk-levels">
                    <div class="risk-level entry">Entry<br>Giá hiện tại</div>
                    <div class="risk-level sl">Stop Loss<br>ATR × 3.5</div>
                    <div class="risk-level tp1">TP1<br>SL × 1.1</div>
                    <div class="risk-level tp2">TP2<br>SL × 1.65</div>
                    <div class="risk-level tp3">TP3<br>SL × 2.2</div>
                </div>
            </div>

            <!-- Multi-timeframe -->
            <div class="card">
                <h2>⏰ Bảng Multi-Timeframe</h2>
                <p>Chỉ báo hiển thị xu hướng của 9 khung thời gian khác nhau:</p>
                
                <table class="timeframe-table">
                    <thead>
                        <tr>
                            <th>TF</th>
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
                            <td class="trend-down">DN</td>
                            <td class="trend-down">DN</td>
                            <td class="trend-up">UP</td>
                            <td class="trend-up">UP</td>
                            <td class="trend-up">UP</td>
                            <td class="trend-up">UP</td>
                            <td class="trend-up">UP</td>
                        </tr>
                    </tbody>
                </table>

                <div style="margin-top: 15px;">
                    <p><strong>🟢 UP:</strong> EMA21 > EMA89 (xu hướng tăng)</p>
                    <p><strong>🔴 DN:</strong> EMA21 < EMA89 (xu hướng giảm)</p>
                </div>
            </div>

            <!-- Chiến lược -->
            <div class="card">
                <h2>💡 Chiến lược giao dịch</h2>
                
                <h3>🎯 Chiến lược cơ bản:</h3>
                <div class="step-list">
                    <div class="step">
                        <strong>Xác định xu hướng chính</strong>
                        <p>Kiểm tra bảng multi-timeframe, ưu tiên các TF cao hơn (H4, D1, W1)</p>
                    </div>
                    <div class="step">
                        <strong>Chờ tín hiệu cùng chiều</strong>
                        <p>Chỉ vào lệnh khi tín hiệu cùng hướng với xu hướng chính</p>
                    </div>
                    <div class="step">
                        <strong>Quản lý lệnh</strong>
                        <p>Sử dụng các mức TP/SL tự động hoặc điều chỉnh theo RR 1:2</p>
                    </div>
                    <div class="step">
                        <strong>Exit chiến lược</strong>
                        <p>Thoát lệnh khi có tín hiệu ngược chiều hoặc chạm TP/SL</p>
                    </div>
                </div>

                <div class="warning">
                    <h3>📊 Phân bổ lệnh khuyến nghị:</h3>
                    <p><strong>TP1:</strong> 50% volume (chốt lời nhanh)</p>
                    <p><strong>TP2:</strong> 30% volume (mục tiêu chính)</p>
                    <p><strong>TP3:</strong> 20% volume (để chạy trend)</p>
                </div>
            </div>

            <!-- Lưu ý -->
            <div class="card">
                <h2>⚠️ Lưu ý quan trọng</h2>
                
                <div class="warning">
                    <h3>🚫 Tránh giao dịch khi:</h3>
                    <ul style="margin-left: 20px; margin-top: 10px;">
                        <li>Thị trường sideway (không có xu hướng rõ ràng)</li>
                        <li>Trước/sau các sự kiện tin tức quan trọng</li>
                        <li>Volume thấp hoặc thanh khoản kém</li>
                        <li>Các khung thời gian mâu thuẫn nhau</li>
                    </ul>
                </div>

                <div class="highlight">
                    <h3>💰 Quản lý rủi ro:</h3>
                    <p>• Không rủi ro quá 2-3% tài khoản mỗi lệnh</p>
                    <p>• Sử dụng position sizing phù hợp</p>
                    <p>• Luôn đặt Stop Loss</p>
                    <p>• Không trade quá nhiều lệnh cùng lúc</p>
                    <p>• Backtest trước khi trade thực</p>
                </div>
            </div>

            <!-- FAQ -->
            <div class="card">
                <h2>❓ Câu hỏi thường gặp</h2>
                
                <div style="margin-top: 20px;">
                    <strong>Q: Chỉ báo này phù hợp với timeframe nào?</strong>
                    <p>A: Mọi timeframe từ M1 đến MN, nhưng hiệu quả nhất trên M15-H4.</p>
                </div>

                <div style="margin-top: 20px;">
                    <strong>Q: Có thể dùng cho mọi cặp tiền tệ?</strong>
                    <p>A: Có, nhưng nên điều chỉnh tham số phù hợp với volatility của từng cặp.</p>
                </div>

                <div style="margin-top: 20px;">
                    <strong>Q: Tại sao có tín hiệu sai?</strong>
                    <p>A: Không có chỉ báo nào 100% chính xác. Cần kết hợp phân tích tổng thể và quản lý rủi ro.</p>
                </div>

                <div style="margin-top: 20px;">
                    <strong>Q: Có thể sử dụng cho crypto không?</strong>
                    <p>A: Có, nhưng cần giảm Sensitivity do crypto có volatility cao.</p>
                </div>
            </div>
        </div>

        <footer class="footer">
            <p>© 2024 T4U Algo V3.7 - Hướng dẫn sử dụng chỉ báo trading chuyên nghiệp</p>
            <p style="opacity: 0.8; margin-top: 10px;">
                ⚠️ Trading có rủi ro - Luôn quản lý vốn cẩn thận
            </p>
        </footer>
    </div>

    <script>
        // Smooth scrolling animation
        document.addEventListener('DOMContentLoaded', function() {
            const cards = document.querySelectorAll('.card');
            
            const observerOptions = {
                threshold: 0.1,
                rootMargin: '0px 0px -50px 0px'
            };

            const observer = new IntersectionObserver(function(entries) {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.style.opacity = '0';
                        entry.target.style.transform = 'translateY(30px)';
                        entry.target.style.transition = 'all 0.6s ease';
                        
                        setTimeout(() => {
                            entry.target.style.opacity = '1';
                            entry.target.style.transform = 'translateY(0)';
                        }, 100);
                    }
                });
            }, observerOptions);

            cards.forEach(card => {
                observer.observe(card);
            });

            // Add click animation to features
            const features = document.querySelectorAll('.feature');
            features.forEach(feature => {
                feature.addEventListener('click', function() {
                    this.style.transform = 'scale(0.95)';
                    setTimeout(() => {
                        this.style.transform = 'scale(1.02)';
                    }, 150);
                });
            });

            // Interactive trend table
            const trendCells = document.querySelectorAll('.trend-up, .trend-down');
            trendCells.forEach(cell => {
                cell.addEventListener('mouseover', function() {
                    this.style.transform = 'scale(1.1)';
                    this.style.transition = 'transform 0.2s ease';
                });
                
                cell.addEventListener('mouseout', function() {
                    this.style.transform = 'scale(1)';
                });
            });
        });
    </script>
</body>
</html>
