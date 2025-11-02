
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FreeDivingLog - Apple Watch Ultra 2 UI Mockup</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
            padding: 40px 20px;
            min-height: 100vh;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        h1 {
            text-align: center;
            color: #ffffff;
            font-size: 32px;
            margin-bottom: 40px;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
        }

        .screens-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
            margin-bottom: 40px;
        }

        .watch-frame {
            background: linear-gradient(145deg, #2d2d2d, #1a1a1a);
            border-radius: 60px;
            padding: 20px;
            box-shadow: 
                0 20px 60px rgba(0, 0, 0, 0.6),
                inset 0 1px 2px rgba(255, 255, 255, 0.1);
            position: relative;
        }

        .watch-frame::before {
            content: '';
            position: absolute;
            top: 50%;
            right: -8px;
            transform: translateY(-50%);
            width: 8px;
            height: 50px;
            background: linear-gradient(90deg, #3a3a3a, #2a2a2a);
            border-radius: 0 4px 4px 0;
        }

        .screen-label {
            text-align: center;
            color: #888;
            font-size: 11px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 12px;
        }

        .watch-screen {
            background: #000000;
            border-radius: 45px;
            width: 100%;
            aspect-ratio: 1;
            padding: 24px;
            display: flex;
            flex-direction: column;
            color: white;
            position: relative;
            overflow: hidden;
            font-size: 14px;
        }

        .screen-header {
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 16px;
            font-size: 13px;
            font-weight: 600;
            color: #888;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            animation: pulse 2s infinite;
        }

        .status-dot.green { background: #00ff88; }
        .status-dot.red { background: #ff3b30; }
        .status-dot.blue { background: #0a84ff; }
        .status-dot.yellow { background: #ffd60a; }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        .divider {
            height: 1px;
            background: linear-gradient(90deg, transparent, #333, transparent);
            margin: 12px 0;
        }

        .main-value {
            text-align: center;
            font-size: 56px;
            font-weight: 700;
            line-height: 1;
            margin: 20px 0;
            letter-spacing: -2px;
            text-shadow: 0 0 20px currentColor;
        }

        .main-value.large {
            font-size: 64px;
        }

        .info-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px 0;
            font-size: 13px;
        }

        .info-label {
            color: #888;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .info-value {
            font-weight: 600;
            color: #ffffff;
        }

        .pb-badge {
            display: inline-block;
            background: linear-gradient(135deg, #ffd700, #ffed4e);
            color: #000;
            padding: 2px 8px;
            border-radius: 8px;
            font-size: 11px;
            font-weight: 700;
            margin-left: 6px;
        }

        .button {
            background: linear-gradient(135deg, #0a84ff, #0066cc);
            color: white;
            border: none;
            padding: 14px 20px;
            border-radius: 24px;
            font-size: 15px;
            font-weight: 600;
            text-align: center;
            margin-top: auto;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(10, 132, 255, 0.4);
        }

        .button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(10, 132, 255, 0.6);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin: 12px 0;
        }

        .stat-box {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 12px;
            padding: 10px;
            text-align: center;
        }

        .stat-label {
            font-size: 10px;
            color: #888;
            margin-bottom: 4px;
        }

        .stat-value {
            font-size: 18px;
            font-weight: 700;
            color: #fff;
        }

        .alert-banner {
            background: rgba(255, 59, 48, 0.2);
            border: 2px solid #ff3b30;
            border-radius: 16px;
            padding: 12px;
            text-align: center;
            margin: 12px 0;
            animation: alertPulse 1s infinite;
        }

        @keyframes alertPulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        .alert-title {
            font-size: 13px;
            font-weight: 700;
            color: #ff3b30;
            margin-bottom: 6px;
        }

        .warning-banner {
            background: rgba(255, 214, 10, 0.15);
            border: 2px solid #ffd60a;
            border-radius: 16px;
            padding: 10px;
            text-align: center;
            margin: 12px 0;
        }

        .warning-title {
            font-size: 12px;
            font-weight: 700;
            color: #ffd60a;
            margin-bottom: 4px;
        }

        .success-badge {
            background: rgba(0, 255, 136, 0.15);
            border: 2px solid #00ff88;
            border-radius: 16px;
            padding: 10px;
            text-align: center;
            margin: 12px 0;
        }

        .success-title {
            font-size: 13px;
            font-weight: 700;
            color: #00ff88;
        }

        .timer-display {
            text-align: center;
            margin: 16px 0;
        }

        .timer-label {
            font-size: 11px;
            color: #888;
            margin-bottom: 6px;
        }

        .timer-value {
            font-size: 48px;
            font-weight: 700;
            color: #0a84ff;
            line-height: 1;
        }

        .bg-alert {
            background: linear-gradient(135deg, #1a0000, #330000) !important;
        }

        .bg-success {
            background: linear-gradient(135deg, #001a0a, #003314) !important;
        }

        .bg-warning {
            background: linear-gradient(135deg, #1a1700, #332e00) !important;
        }

        .setting-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }

        .setting-label {
            font-size: 13px;
            color: #fff;
        }

        .setting-value {
            font-size: 14px;
            font-weight: 600;
            color: #0a84ff;
        }

        .legend {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 16px;
            padding: 20px;
            margin-top: 30px;
            color: #fff;
        }

        .legend h3 {
            font-size: 18px;
            margin-bottom: 16px;
            color: #0a84ff;
        }

        .legend-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 16px;
        }

        .legend-item {
            display: flex;
            align-items: flex-start;
            gap: 12px;
        }

        .legend-icon {
            width: 24px;
            height: 24px;
            border-radius: 6px;
            flex-shrink: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
        }

        .legend-text {
            flex: 1;
        }

        .legend-title {
            font-size: 13px;
            font-weight: 600;
            margin-bottom: 4px;
        }

        .legend-desc {
            font-size: 11px;
            color: #888;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>⌚ FreeDivingLog - Apple Watch Ultra 2 UI Mockup</h1>
        
        <div class="screens-grid">
            <!-- 1. Home Screen -->
            <div class="watch-frame">
                <div class="screen-label">🏠 Home Screen</div>
                <div class="watch-screen">
                    <div class="screen-header">
                        <span class="status-dot green"></span>
                        <span>READY</span>
                    </div>
                    
                    <div style="text-align: center; margin-bottom: 16px;">
                        <div style="font-size: 18px; font-weight: 600;">👤 John Freediver</div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="margin: 16px 0;">
                        <div style="font-size: 12px; color: #888; margin-bottom: 8px;">📊 PERSONAL BEST</div>
                        <div class="info-row">
                            <span class="info-label">🏆 Max Depth</span>
                            <span class="info-value">42.3m</span>
                        </div>
                        <div class="info-row">
                            <span class="info-label">⏱️ Max Time</span>
                            <span class="info-value">3:45</span>
                        </div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="margin: 16px 0;">
                        <div style="font-size: 12px; color: #888; margin-bottom: 8px;">⚙️ Quick Settings</div>
                        <div class="info-row">
                            <span class="info-label">🎯 Target</span>
                            <span class="info-value">40m</span>
                        </div>
                        <div class="info-row">
                            <span class="info-label">⏲️ Recovery</span>
                            <span class="info-value">2:00</span>
                        </div>
                    </div>
                    
                    <button class="button">🌊 START DIVE</button>
                </div>
            </div>

            <!-- 2. Pre-Dive Screen -->
            <div class="watch-frame">
                <div class="screen-label">🔵 Pre-Dive</div>
                <div class="watch-screen">
                    <div class="screen-header">
                        <span class="status-dot blue"></span>
                        <span>PRE-DIVE</span>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="info-row">
                        <span class="info-label">📍 Location</span>
                        <span class="info-value" style="color: #00ff88;">Ready</span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">🌡️ Water Temp</span>
                        <span class="info-value">24°C</span>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="margin: 16px 0;">
                        <div style="font-size: 12px; color: #888; margin-bottom: 8px;">⚙️ Session Settings</div>
                        <div class="info-row">
                            <span class="info-label">🎯 Target</span>
                            <span class="info-value">40m</span>
                        </div>
                        <div class="info-row">
                            <span class="info-label">⏲️ Recovery</span>
                            <span class="info-value">2:00</span>
                        </div>
                        <div class="info-row">
                            <span class="info-label">🔔 Alerts</span>
                            <span class="info-value" style="color: #00ff88;">ON</span>
                        </div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="text-align: center; margin-top: auto; padding: 16px 0; color: #00ff88; font-size: 13px;">
                        ✅ Ready to Dive<br>
                        <span style="font-size: 11px; color: #666;">(1m depth auto-start)</span>
                    </div>
                </div>
            </div>

            <!-- 3. Active Dive Screen -->
            <div class="watch-frame">
                <div class="screen-label">🟢 Active Dive</div>
                <div class="watch-screen bg-success">
                    <div class="screen-header">
                        <span class="status-dot green"></span>
                        <span>DIVING</span>
                    </div>
                    
                    <div class="main-value large" style="color: #00ff88;">38.5m</div>
                    
                    <div class="divider"></div>
                    
                    <div class="info-row">
                        <span class="info-label">⏱️ Time</span>
                        <span class="info-value" style="font-size: 18px;">2:15</span>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="info-row">
                        <span class="info-label">🎯 Target</span>
                        <span class="info-value">40m</span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">↑ Ascent</span>
                        <span class="info-value" style="color: #00ff88;">0.8 m/s</span>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="info-row" style="font-size: 12px;">
                        <span class="info-label">💓 Heart</span>
                        <span class="info-value">65 bpm</span>
                    </div>
                    <div class="info-row" style="font-size: 12px;">
                        <span class="info-label">🌡️ Temp</span>
                        <span class="info-value">24°C</span>
                    </div>
                </div>
            </div>

            <!-- 4. Alert Screen -->
            <div class="watch-frame">
                <div class="screen-label">🔴 Alert</div>
                <div class="watch-screen bg-alert">
                    <div class="screen-header">
                        <span class="status-dot red"></span>
                        <span>ALERT!</span>
                    </div>
                    
                    <div class="main-value large" style="color: #ffffff;">38.5m</div>
                    
                    <div class="divider"></div>
                    
                    <div class="alert-banner">
                        <div class="alert-title">⚠️ ASCENT SPEED</div>
                        <div style="font-size: 36px; font-weight: 700; color: #ff3b30; margin: 8px 0;">1.5 m/s</div>
                        <div style="font-size: 14px; font-weight: 700; color: #ff3b30;">TOO FAST!</div>
                    </div>
                    
                    <div style="text-align: center; color: #ff6b6b; font-size: 12px; margin-top: 16px;">
                        📳 Strong Haptic x3<br>
                        Slow down your ascent
                    </div>
                </div>
            </div>

            <!-- 5. Target Reached -->
            <div class="watch-frame">
                <div class="screen-label">🎯 Target Reached</div>
                <div class="watch-screen bg-success">
                    <div class="screen-header">
                        <span class="status-dot green"></span>
                        <span>TARGET!</span>
                    </div>
                    
                    <div class="main-value large" style="color: #00ff88;">40.0m</div>
                    
                    <div class="divider"></div>
                    
                    <div class="success-badge">
                        <div class="success-title">✅ Goal Achieved!</div>
                        <div style="font-size: 11px; color: #888; margin-top: 4px;">Target depth reached</div>
                    </div>
                    
                    <div class="info-row" style="margin-top: 16px;">
                        <span class="info-label">⏱️ Time</span>
                        <span class="info-value" style="font-size: 18px;">2:20</span>
                    </div>
                    
                    <div style="text-align: center; color: #00ff88; font-size: 12px; margin-top: 16px;">
                        📳 Haptic x2<br>
                        <span style="color: #666;">Returns to dive mode in 1s</span>
                    </div>
                </div>
            </div>

            <!-- 6. Surface Mode -->
            <div class="watch-frame">
                <div class="screen-label">🌊 Surface</div>
                <div class="watch-screen">
                    <div class="screen-header">
                        <span class="status-dot blue"></span>
                        <span>SURFACE</span>
                    </div>
                    
                    <div style="text-align: center; font-size: 13px; color: #888; margin-bottom: 8px;">
                        Dive #3 Complete
                    </div>
                    
                    <div class="stats-grid">
                        <div class="stat-box">
                            <div class="stat-label">Max Depth</div>
                            <div class="stat-value">40.2m <span class="pb-badge">PB</span></div>
                        </div>
                        <div class="stat-box">
                            <div class="stat-label">Time</div>
                            <div class="stat-value">2:45</div>
                        </div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="timer-display">
                        <div class="timer-label">⏲️ RECOVERY TIMER</div>
                        <div class="timer-value">1:35</div>
                        <div style="font-size: 11px; color: #666; margin-top: 4px;">(2:00 recommended)</div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="font-size: 11px; color: #888; margin-top: 8px;">
                        <div class="info-row" style="font-size: 11px;">
                            <span>Session Stats:</span>
                        </div>
                        <div class="info-row" style="font-size: 11px;">
                            <span class="info-label">Dives</span>
                            <span class="info-value">3</span>
                        </div>
                        <div class="info-row" style="font-size: 11px;">
                            <span class="info-label">Max</span>
                            <span class="info-value">40.2m</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 7. Recovery Warning -->
            <div class="watch-frame">
                <div class="screen-label">⚠️ Recovery Warning</div>
                <div class="watch-screen bg-warning">
                    <div class="screen-header">
                        <span class="status-dot yellow"></span>
                        <span>SURFACE</span>
                    </div>
                    
                    <div class="timer-display">
                        <div class="timer-label">⏲️ RECOVERY</div>
                        <div class="timer-value" style="color: #ffd60a;">0:45</div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="warning-banner">
                        <div class="warning-title">⚠️ Short Recovery</div>
                        <div style="font-size: 11px; color: #fff; margin-top: 6px;">
                            Recommended: 2:00<br>
                            Current: 0:45
                        </div>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="text-align: center; font-size: 12px; color: #ffd60a; margin-top: 12px;">
                        ⚠️ Take more time<br>
                        <span style="font-size: 11px; color: #888;">for safety</span>
                    </div>
                    
                    <div style="text-align: center; color: #666; font-size: 10px; margin-top: 12px;">
                        📳 Soft Haptic x1
                    </div>
                </div>
            </div>

            <!-- 8. Session Summary -->
            <div class="watch-frame">
                <div class="screen-label">📊 Session Summary</div>
                <div class="watch-screen">
                    <div class="screen-header">
                        <span class="status-dot blue"></span>
                        <span>SESSION END</span>
                    </div>
                    
                    <div style="text-align: center; font-size: 20px; font-weight: 700; margin: 12px 0;">
                        Total Dives: 5
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="info-row">
                        <span class="info-label">🏆 Max Depth</span>
                        <span class="info-value">40.2m <span class="pb-badge">PB</span></span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">⏱️ Max Time</span>
                        <span class="info-value">2:45</span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">📊 Avg Depth</span>
                        <span class="info-value">35.8m</span>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div class="info-row">
                        <span class="info-label">⏲️ Total Time</span>
                        <span class="info-value">12:30</span>
                    </div>
                    <div class="info-row">
                        <span class="info-label">🌡️ Water Temp</span>
                        <span class="info-value">24°C</span>
                    </div>
                    
                    <div class="divider"></div>
                    
                    <div style="text-align: center; color: #00ff88; font-size: 12px; margin: 12px 0;">
                        ✅ Synced to iPhone
                    </div>
                    
                    <button class="button" style="margin-top: 8px;">🏠 Back to Home</button>
                </div>
            </div>

            <!-- 9. Settings -->
            <div class="watch-frame">
                <div class="screen-label">⚙️ Settings</div>
                <div class="watch-screen">
                    <div class="screen-header">
                        <span class="status-dot blue"></span>
                        <span>SETTINGS</span>
                    </div>
                    
                    <div class="setting-row">
                        <div class="setting-label">🎯 Target Depth</div>
                        <div class="setting-value">→ 40m</div>
                    </div>
                    
                    <div class="setting-row">
                        <div class="setting-label">⏲️ Recovery Time</div>
                        <div class="setting-value">→ 2:00</div>
                    </div>
                    
                    <div class="setting-row">
                        <div class="setting-label">🚀 Ascent Alert</div>
                        <div class="setting-value">→ 1.2 m/s</div>
                    </div>
                    
                    <div class="setting-row">
                        <div class="setting-label">🔔 Haptics</div>
                        <div class="setting-value" style="color: #00ff88;">ON</div>
                    </div>
                    
                    <div class="setting-row" style="border-bottom: none;">
                        <div class="setting-label">📏 Units</div>
                        <div class="setting-value">Meters</div>
                    </div>
                    
                    <div style="text-align: center; color: #666; font-size: 10px; margin-top: 16px;">
                        Use Digital Crown to adjust<br>
                        Tap to toggle ON/OFF
                    </div>
                </div>
            </div>
        </div>

        <!-- Legend -->
        <div class="legend">
            <h3>🎨 UI 디자인 가이드라인</h3>
            <div class="legend-grid">
                <div class="legend-item">
                    <div class="legend-icon" style="background: #00ff88;">🟢</div>
                    <div class="legend-text">
                        <div class="legend-title">정상 상태 (Green)</div>
                        <div class="legend-desc">안전한 다이빙 진행 중, 목표 달성</div>
                    </div>
                </div>
                
                <div class="legend-item">
                    <div class="legend-icon" style="background: #ff3b30;">🔴</div>
                    <div class="legend-text">
                        <div class="legend-title">위험 경고 (Red)</div>
                        <div class="legend-desc">상승속도 초과, 즉시 조치 필요</div>
                    </div>
                </div>
                
                <div class="legend-item">
                    <div class="legend-icon" style="background: #ffd60a;">🟡</div>
                    <div class="legend-text">
                        <div class="legend-title">주의 필요 (Yellow)</div>
                        <div class="legend-desc">회복시간 부족, 주의 권고</div>
                    </div>
                </div>
                
                <div class="legend-item">
                    <div class="legend-icon" style="background: #0a84ff;">🔵</div>
                    <div class="legend-text">
                        <div class="legend-title">정보/대기 (Blue)</div>
                        <div class="legend-desc">수면 상태, 준비 모드</div>
                    </div>
                </div>
                
                <div class="legend-item">
                    <div class="legend-icon" style="background: #ffd700;">🏆</div>
                    <div class="legend-text">
                        <div class="legend-title">PB 달성 (Gold)</div>
                        <div class="legend-desc">개인 최고 기록 갱신</div>
                    </div>
                </div>
                
                <div class="legend-item">
                    <div class="legend-icon" style="background: #666;">📳</div>
                    <div class="legend-text">
                        <div class="legend-title">햅틱 피드백</div>
                        <div class="legend-desc">진동 강도: 강함(x3), 중간(x2), 약함(x1)
