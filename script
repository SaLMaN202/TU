-- ========================================
-- TU Single Instance Guard
-- ========================================

if _G.TU_SCRIPT and type(_G.TU_SCRIPT.Stop) == "function" then
    pcall(function()
        _G.TU_SCRIPT:Stop()
    end)
end

local Script = {
    Connections = {},
    Gui = nil,
    Running = true
}

_G.TU_SCRIPT = Script

function Script:Bind(connection)
    table.insert(self.Connections, connection)
    return connection
end

function Script:Stop()
    if not self.Running then return end
    self.Running = false

    for _, connection in ipairs(self.Connections) do
        pcall(function()
            if connection and connection.Disconnect then
                connection:Disconnect()
            end
        end)
    end
    table.clear(self.Connections)

    pcall(function()
        if self.Gui then
            self.Gui:Destroy()
            self.Gui = nil
        end
    end)

    if _G.TU_SCRIPT == self then
        _G.TU_SCRIPT = nil
    end
end

-- ========================================
-- ضع سكربتك الحالي أسفل هذا السطر مباشرة
-- ========================================
local Players          = game:GetService("Players")
local RunService       = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService     = game:GetService("TweenService")
local LocalPlayer      = Players.LocalPlayer
local Mouse            = LocalPlayer:GetMouse()

local SCRIPT_URL = "https://pastebin.com/raw/wJwa54Gj"  

local function SafeTeleport(placeId, jobId, player)
    
    if SCRIPT_URL ~= "" then
        local queueFn = queue_on_teleport or (syn and syn.queue_on_teleport)
        if queueFn then
            pcall(queueFn, ('loadstring(game:HttpGet("%s"))()'):format(SCRIPT_URL))
        end
    end
    task.delay(0.3, function()
        pcall(function()
            game:GetService("TeleportService"):TeleportToPlaceInstance(placeId, jobId, player)
        end)
    end)
end

local function GetChar()  return LocalPlayer.Character end
local function GetHum()
    local c = GetChar()
    return c and c:FindFirstChildOfClass("Humanoid")
end
local function GetRoot()
    local c = GetChar()
    return c and c:FindFirstChild("HumanoidRootPart")
end

local _TP_TARGET = Vector3.new(3.0, 2.8, 812.8)
task.spawn(function()
    local _char = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
    local _root = _char:WaitForChild("HumanoidRootPart", 10)
    if _root then
        _root.CFrame = CFrame.new(_TP_TARGET)
    end
end)

if game.CoreGui:FindFirstChild("EliteAceGUI") then
    game.CoreGui.EliteAceGUI:Destroy()
end

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name            = "EliteAceGUI"
ScreenGui.ResetOnSpawn    = false
ScreenGui.ZIndexBehavior  = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent          = game.CoreGui

local MainFrame = Instance.new("Frame")
MainFrame.Name              = "MainFrame"
MainFrame.Size              = UDim2.new(0, 560, 0, 640)
MainFrame.Position          = UDim2.new(0.5, -280, 0.5, -320)
MainFrame.BackgroundColor3  = Color3.fromRGB(15, 15, 20)
MainFrame.BorderSizePixel   = 0
MainFrame.ClipsDescendants  = true
MainFrame.Parent            = ScreenGui

local Shadow = Instance.new("ImageLabel", MainFrame)
Shadow.Size                 = UDim2.new(1, 30, 1, 30)
Shadow.Position             = UDim2.new(0, -15, 0, -15)
Shadow.BackgroundTransparency = 1
Shadow.Image                = "rbxassetid://5554236805"
Shadow.ImageColor3          = Color3.fromRGB(0, 0, 0)
Shadow.ImageTransparency    = 0.5
Shadow.ScaleType            = Enum.ScaleType.Slice
Shadow.SliceCenter          = Rect.new(23, 23, 277, 277)
Shadow.ZIndex               = 0

local UICorner = Instance.new("UICorner", MainFrame)
UICorner.CornerRadius = UDim.new(0, 12)

local TitleBar = Instance.new("Frame", MainFrame)
TitleBar.Size               = UDim2.new(1, 0, 0, 50)
TitleBar.BackgroundColor3   = Color3.fromRGB(20, 20, 30)
TitleBar.BorderSizePixel    = 0

local TitleCorner = Instance.new("UICorner", TitleBar)
TitleCorner.CornerRadius = UDim.new(0, 12)

local TitleLine = Instance.new("Frame", TitleBar)
TitleLine.Size              = UDim2.new(1, 0, 0, 2)
TitleLine.Position          = UDim2.new(0, 0, 1, -2)
TitleLine.BackgroundColor3  = Color3.fromRGB(100, 60, 220)
TitleLine.BorderSizePixel   = 0

local TitleIcon = Instance.new("TextLabel", TitleBar)
TitleIcon.Size              = UDim2.new(0, 40, 1, 0)
TitleIcon.Position          = UDim2.new(0, 10, 0, 0)
TitleIcon.BackgroundTransparency = 1
TitleIcon.Text              = "🏠"
TitleIcon.TextSize          = 22
TitleIcon.Font              = Enum.Font.GothamBold
TitleIcon.TextXAlignment    = Enum.TextXAlignment.Left

local TitleLabel = Instance.new("TextLabel", TitleBar)
TitleLabel.Size             = UDim2.new(1, -100, 1, 0)
TitleLabel.Position         = UDim2.new(0, 50, 0, 0)
TitleLabel.BackgroundTransparency = 1

if syn and syn.protect_gui then
    syn.protect_gui(ScreenGui)
    ScreenGui.Parent = game:GetService("CoreGui")
elseif gethui then
    ScreenGui.Parent = gethui()
else
    local ok = pcall(function() ScreenGui.Parent = game:GetService("CoreGui") end)
    if not ok then ScreenGui.Parent = LocalPlayer.PlayerGui end
end
TitleLabel.TextColor3       = Color3.fromRGB(255, 255, 255)
TitleLabel.TextSize         = 15
TitleLabel.Font             = Enum.Font.GothamBold
TitleLabel.TextXAlignment   = Enum.TextXAlignment.Left

local CloseBtn = Instance.new("TextButton", TitleBar)
CloseBtn.Size               = UDim2.new(0, 30, 0, 30)
CloseBtn.Position           = UDim2.new(1, -38, 0.5, -15)
CloseBtn.BackgroundColor3   = Color3.fromRGB(200, 50, 50)
CloseBtn.Text               = "✕"
CloseBtn.TextColor3         = Color3.fromRGB(255, 255, 255)
CloseBtn.TextSize           = 14
CloseBtn.Font               = Enum.Font.GothamBold
CloseBtn.BorderSizePixel    = 0
local CloseCorner = Instance.new("UICorner", CloseBtn)
CloseCorner.CornerRadius = UDim.new(0, 6)

local MinBtn = Instance.new("TextButton", TitleBar)
MinBtn.Size                 = UDim2.new(0, 30, 0, 30)
MinBtn.Position             = UDim2.new(1, -74, 0.5, -15)
MinBtn.BackgroundColor3     = Color3.fromRGB(60, 60, 80)
MinBtn.Text                 = "—"
MinBtn.TextColor3           = Color3.fromRGB(255, 255, 255)
MinBtn.TextSize             = 14
MinBtn.Font                 = Enum.Font.GothamBold
MinBtn.BorderSizePixel      = 0
local MinCorner = Instance.new("UICorner", MinBtn)
MinCorner.CornerRadius = UDim.new(0, 6)

local TabBar = Instance.new("Frame", MainFrame)
TabBar.Size               = UDim2.new(1, 0, 0, 36)
TabBar.Position           = UDim2.new(0, 0, 0, 50)
TabBar.BackgroundColor3   = Color3.fromRGB(18, 18, 26)
TabBar.BorderSizePixel    = 0

local TabLayout = Instance.new("UIListLayout", TabBar)
TabLayout.FillDirection       = Enum.FillDirection.Horizontal
TabLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
TabLayout.Padding             = UDim.new(0, 4)

local TabPad = Instance.new("UIPadding", TabBar)
TabPad.PaddingLeft  = UDim.new(0, 8)
TabPad.PaddingRight = UDim.new(0, 8)
TabPad.PaddingTop   = UDim.new(0, 5)

local TabLine = Instance.new("Frame", MainFrame)
TabLine.Size              = UDim2.new(1, 0, 0, 2)
TabLine.Position          = UDim2.new(0, 0, 0, 86)
TabLine.BackgroundColor3  = Color3.fromRGB(100, 60, 220)
TabLine.BorderSizePixel   = 0

local ActiveTabBtn = nil
local TabPages = {}

local function MakeTabBtn(label, isFirst)
    local Btn = Instance.new("TextButton", TabBar)
    Btn.Size               = UDim2.new(0, 103, 0, 28)
    Btn.BackgroundColor3   = isFirst and Color3.fromRGB(100, 60, 220) or Color3.fromRGB(30, 30, 44)
    Btn.Text               = label
    Btn.TextColor3         = isFirst and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(160, 160, 190)
    Btn.TextSize           = 12
    Btn.Font               = Enum.Font.GothamBold
    Btn.BorderSizePixel    = 0
    local BC = Instance.new("UICorner", Btn)
    BC.CornerRadius = UDim.new(0, 7)
    return Btn
end

local function MakePage()
    local Page = Instance.new("ScrollingFrame", MainFrame)
    Page.Size                  = UDim2.new(1, 0, 1, -90)
    Page.Position              = UDim2.new(0, 0, 0, 90)
    Page.BackgroundTransparency = 1
    Page.BorderSizePixel       = 0
    Page.ScrollBarThickness    = 3
    Page.ScrollBarImageColor3  = Color3.fromRGB(100, 60, 220)
    Page.CanvasSize            = UDim2.new(0, 0, 0, 0)
    Page.Visible               = false

    local Layout = Instance.new("UIListLayout", Page)
    Layout.Padding            = UDim.new(0, 6)
    Layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
    Layout.SortOrder          = Enum.SortOrder.LayoutOrder

    local Pad = Instance.new("UIPadding", Page)
    Pad.PaddingTop    = UDim.new(0, 10)
    Pad.PaddingBottom = UDim.new(0, 10)

    Layout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
        Page.CanvasSize = UDim2.new(0, 0, 0, Layout.AbsoluteContentSize.Y + 20)
    end)

    return Page, Layout
end

local PagePlayer,  LayoutPlayer  = MakePage()
local PageNetwork, LayoutNetwork = MakePage()
local PageScript,  LayoutScript  = MakePage()
local PageHub,     LayoutHub     = MakePage()

local BtnPlayer  = MakeTabBtn("👤 Player",  true)
local BtnNetwork = MakeTabBtn("🖥️ Server",  false)
local BtnScript  = MakeTabBtn("📜 Script",  false)
local BtnHub     = MakeTabBtn("🌐 Hub",     false)

local PageScanner = Instance.new("ScrollingFrame", MainFrame)
PageScanner.Size                  = UDim2.new(1, 0, 1, -90)
PageScanner.Position              = UDim2.new(0, 0, 0, 90)
PageScanner.BackgroundTransparency = 1
PageScanner.BorderSizePixel       = 0
PageScanner.ScrollBarThickness    = 0
PageScanner.CanvasSize            = UDim2.new(0, 0, 0, 0)
PageScanner.Visible               = false
PageScanner.ClipsDescendants      = true

local BtnScanner = MakeTabBtn("🔍 Scanner", false)

local function SwitchTab(btn, page)
    for _, b in pairs({BtnPlayer, BtnNetwork, BtnScript, BtnScanner, BtnHub}) do
        TweenService:Create(b, TweenInfo.new(0.15), {
            BackgroundColor3 = Color3.fromRGB(30, 30, 44),
            TextColor3       = Color3.fromRGB(160, 160, 190)
        }):Play()
    end
    for _, p in pairs({PagePlayer, PageNetwork, PageScript, PageScanner, PageHub}) do
        p.Visible = false
    end
    TweenService:Create(btn, TweenInfo.new(0.15), {
        BackgroundColor3 = Color3.fromRGB(100, 60, 220),
        TextColor3       = Color3.fromRGB(255, 255, 255)
    }):Play()
    page.Visible = true
end

BtnPlayer.MouseButton1Click:Connect(function()  SwitchTab(BtnPlayer,  PagePlayer)  end)
BtnNetwork.MouseButton1Click:Connect(function() SwitchTab(BtnNetwork, PageNetwork) end)
BtnScript.MouseButton1Click:Connect(function()  SwitchTab(BtnScript,  PageScript)  end)
BtnScanner.MouseButton1Click:Connect(function() SwitchTab(BtnScanner, PageScanner) end)
BtnHub.MouseButton1Click:Connect(function()     SwitchTab(BtnHub,     PageHub)     end)

PagePlayer.Visible = true

local function MakeSection(parent, title)
    local Section = Instance.new("Frame", parent)
    Section.Size               = UDim2.new(0, 530, 0, 28)
    Section.BackgroundColor3   = Color3.fromRGB(30, 30, 45)
    Section.BorderSizePixel    = 0
    local SC = Instance.new("UICorner", Section)
    SC.CornerRadius = UDim.new(0, 7)

    local Lbl = Instance.new("TextLabel", Section)
    Lbl.Size                   = UDim2.new(1, -10, 1, 0)
    Lbl.Position               = UDim2.new(0, 10, 0, 0)
    Lbl.BackgroundTransparency = 1
    Lbl.Text                   = title
    Lbl.TextColor3             = Color3.fromRGB(170, 120, 255)
    Lbl.TextSize               = 12
    Lbl.Font                   = Enum.Font.GothamBold
    Lbl.TextXAlignment         = Enum.TextXAlignment.Left
    return Section
end

local function MakeToggle(parent, labelText, defaultState, callback)
    local Row = Instance.new("Frame", parent)
    Row.Size               = UDim2.new(0, 530, 0, 38)
    Row.BackgroundColor3   = Color3.fromRGB(22, 22, 32)
    Row.BorderSizePixel    = 0
    local RC = Instance.new("UICorner", Row)
    RC.CornerRadius = UDim.new(0, 8)

    local Lbl = Instance.new("TextLabel", Row)
    Lbl.Size               = UDim2.new(1, -60, 1, 0)
    Lbl.Position           = UDim2.new(0, 12, 0, 0)
    Lbl.BackgroundTransparency = 1
    Lbl.Text               = labelText
    Lbl.TextColor3         = Color3.fromRGB(210, 210, 230)
    Lbl.TextSize           = 13
    Lbl.Font               = Enum.Font.Gotham
    Lbl.TextXAlignment     = Enum.TextXAlignment.Left

    local ToggleBG = Instance.new("Frame", Row)
    ToggleBG.Size          = UDim2.new(0, 44, 0, 22)
    ToggleBG.Position      = UDim2.new(1, -54, 0.5, -11)
    ToggleBG.BackgroundColor3 = defaultState and Color3.fromRGB(100, 60, 220) or Color3.fromRGB(50, 50, 65)
    ToggleBG.BorderSizePixel = 0
    local TBC = Instance.new("UICorner", ToggleBG)
    TBC.CornerRadius = UDim.new(1, 0)

    local Ball = Instance.new("Frame", ToggleBG)
    Ball.Size              = UDim2.new(0, 16, 0, 16)
    Ball.Position          = defaultState and UDim2.new(1, -19, 0.5, -8) or UDim2.new(0, 3, 0.5, -8)
    Ball.BackgroundColor3  = Color3.fromRGB(255, 255, 255)
    Ball.BorderSizePixel   = 0
    local BC = Instance.new("UICorner", Ball)
    BC.CornerRadius = UDim.new(1, 0)

    local State = defaultState
    local function Toggle()
        State = not State
        TweenService:Create(ToggleBG, TweenInfo.new(0.2), {
            BackgroundColor3 = State and Color3.fromRGB(100, 60, 220) or Color3.fromRGB(50, 50, 65)
        }):Play()
        TweenService:Create(Ball, TweenInfo.new(0.2), {
            Position = State and UDim2.new(1, -19, 0.5, -8) or UDim2.new(0, 3, 0.5, -8)
        }):Play()
        callback(State)
    end

    Row.InputBegan:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1 then Toggle() end
    end)
    ToggleBG.InputBegan:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1 then Toggle() end
    end)

    return Row, function() return State end
end

local function MakeSlider(parent, labelText, minVal, maxVal, defaultVal, callback)
    local Row = Instance.new("Frame", parent)
    Row.Size               = UDim2.new(0, 530, 0, 54)
    Row.BackgroundColor3   = Color3.fromRGB(22, 22, 32)
    Row.BorderSizePixel    = 0
    local RC = Instance.new("UICorner", Row)
    RC.CornerRadius = UDim.new(0, 8)

    local Lbl = Instance.new("TextLabel", Row)
    Lbl.Size               = UDim2.new(1, -60, 0, 22)
    Lbl.Position           = UDim2.new(0, 12, 0, 4)
    Lbl.BackgroundTransparency = 1
    Lbl.Text               = labelText
    Lbl.TextColor3         = Color3.fromRGB(210, 210, 230)
    Lbl.TextSize           = 13
    Lbl.Font               = Enum.Font.Gotham
    Lbl.TextXAlignment     = Enum.TextXAlignment.Left

    local ValLbl = Instance.new("TextLabel", Row)
    ValLbl.Size            = UDim2.new(0, 50, 0, 22)
    ValLbl.Position        = UDim2.new(1, -58, 0, 4)
    ValLbl.BackgroundTransparency = 1
    ValLbl.Text            = tostring(defaultVal)
    ValLbl.TextColor3      = Color3.fromRGB(170, 120, 255)
    ValLbl.TextSize        = 13
    ValLbl.Font            = Enum.Font.GothamBold
    ValLbl.TextXAlignment  = Enum.TextXAlignment.Right

    local Track = Instance.new("Frame", Row)
    Track.Size             = UDim2.new(1, -24, 0, 6)
    Track.Position         = UDim2.new(0, 12, 0, 36)
    Track.BackgroundColor3 = Color3.fromRGB(40, 40, 55)
    Track.BorderSizePixel  = 0
    local TrackC = Instance.new("UICorner", Track)
    TrackC.CornerRadius = UDim.new(1, 0)

    local Fill = Instance.new("Frame", Track)
    local pct = (defaultVal - minVal) / (maxVal - minVal)
    Fill.Size              = UDim2.new(pct, 0, 1, 0)
    Fill.BackgroundColor3  = Color3.fromRGB(100, 60, 220)
    Fill.BorderSizePixel   = 0
    local FillC = Instance.new("UICorner", Fill)
    FillC.CornerRadius = UDim.new(1, 0)

    local Knob = Instance.new("Frame", Track)
    Knob.Size              = UDim2.new(0, 14, 0, 14)
    Knob.Position          = UDim2.new(pct, -7, 0.5, -7)
    Knob.BackgroundColor3  = Color3.fromRGB(255, 255, 255)
    Knob.BorderSizePixel   = 0
    local KnobC = Instance.new("UICorner", Knob)
    KnobC.CornerRadius = UDim.new(1, 0)

    local dragging = false
    Knob.InputBegan:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1 then dragging = true end
    end)
    UserInputService.InputEnded:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1 then dragging = false end
    end)
    UserInputService.InputChanged:Connect(function(i)
        if dragging and i.UserInputType == Enum.UserInputType.MouseMovement then
            local trackPos = Track.AbsolutePosition.X
            local trackSize = Track.AbsoluteSize.X
            local relX = math.clamp((Mouse.X - trackPos) / trackSize, 0, 1)
            local val = math.floor(minVal + (maxVal - minVal) * relX)
            Fill.Size    = UDim2.new(relX, 0, 1, 0)
            Knob.Position = UDim2.new(relX, -7, 0.5, -7)
            ValLbl.Text  = tostring(val)
            callback(val)
        end
    end)
    Track.InputBegan:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1 then
            local trackPos = Track.AbsolutePosition.X
            local trackSize = Track.AbsoluteSize.X
            local relX = math.clamp((Mouse.X - trackPos) / trackSize, 0, 1)
            local val = math.floor(minVal + (maxVal - minVal) * relX)
            Fill.Size    = UDim2.new(relX, 0, 1, 0)
            Knob.Position = UDim2.new(relX, -7, 0.5, -7)
            ValLbl.Text  = tostring(val)
            callback(val)
        end
    end)
    return Row
end

local function MakeButton(parent, labelText, color, callback)
    local Btn = Instance.new("TextButton", parent)
    Btn.Size               = UDim2.new(0, 530, 0, 36)
    Btn.BackgroundColor3   = color or Color3.fromRGB(100, 60, 220)
    Btn.Text               = labelText
    Btn.TextColor3         = Color3.fromRGB(255, 255, 255)
    Btn.TextSize           = 13
    Btn.Font               = Enum.Font.GothamBold
    Btn.BorderSizePixel    = 0
    local BC = Instance.new("UICorner", Btn)
    BC.CornerRadius = UDim.new(0, 8)

    Btn.MouseButton1Click:Connect(function()
        TweenService:Create(Btn, TweenInfo.new(0.1), {
            BackgroundColor3 = Color3.fromRGB(70, 40, 160)
        }):Play()
        task.delay(0.15, function()
            TweenService:Create(Btn, TweenInfo.new(0.1), {
                BackgroundColor3 = color or Color3.fromRGB(100, 60, 220)
            }):Play()
        end)
        callback()
    end)
    return Btn
end

do
    local _row1 = Instance.new("Frame", PagePlayer)
    _row1.Size                   = UDim2.new(0, 530, 0, 36)
    _row1.BackgroundTransparency = 1
    _row1.LayoutOrder            = -4
    local _rl = Instance.new("UIListLayout", _row1)
    _rl.FillDirection       = Enum.FillDirection.Horizontal
    _rl.HorizontalAlignment = Enum.HorizontalAlignment.Center
    _rl.Padding             = UDim.new(0, 10)
    _rl.SortOrder           = Enum.SortOrder.LayoutOrder

        do
            local _b = Instance.new("TextButton", _row1)
            _b.Size             = UDim2.new(0, 260, 1, 0)
            _b.BackgroundColor3 = Color3.fromRGB(20, 90, 160)
            _b.Text             = "🔄 Char"
            _b.TextColor3       = Color3.fromRGB(255, 255, 255)
            _b.TextSize         = 12
            _b.Font             = Enum.Font.GothamBold
            _b.BorderSizePixel  = 0
            Instance.new("UICorner", _b).CornerRadius = UDim.new(0, 8)
            _b.MouseButton1Click:Connect(function()
                local vim = game:GetService("VirtualInputManager")
                local UIS = game:GetService("UserInputService")
                TweenService:Create(_b, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(70, 40, 160)}):Play()
                task.delay(0.15, function()
                    TweenService:Create(_b, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(20, 90, 160)}):Play()
                end)
                vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
                task.wait(0.2)
                local cmdBox = UIS:GetFocusedTextBox()
                if cmdBox then
                    cmdBox.Text = cmdBox.Text .. "char"
                    cmdBox.CursorPosition = #cmdBox.Text + 1
                end
                task.wait(0.05)
                vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
                task.wait(0.05)
                vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
            end)
        end

        do
            local _b = Instance.new("TextButton", _row1)
            _b.Size             = UDim2.new(0, 260, 1, 0)
            _b.BackgroundColor3 = Color3.fromRGB(20, 90, 160)
            _b.Text             = "↩️ Unchar"
            _b.TextColor3       = Color3.fromRGB(255, 255, 255)
            _b.TextSize         = 12
            _b.Font             = Enum.Font.GothamBold
            _b.BorderSizePixel  = 0
            Instance.new("UICorner", _b).CornerRadius = UDim.new(0, 8)
            _b.MouseButton1Click:Connect(function()
                local vim = game:GetService("VirtualInputManager")
                local UIS = game:GetService("UserInputService")
                TweenService:Create(_b, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(70, 40, 160)}):Play()
                task.delay(0.15, function()
                    TweenService:Create(_b, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(20, 90, 160)}):Play()
                end)
                vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
                task.wait(0.2)
                local cmdBox = UIS:GetFocusedTextBox()
                if cmdBox then
                    cmdBox.Text = cmdBox.Text .. "unchar"
                    cmdBox.CursorPosition = #cmdBox.Text + 1
                end
                task.wait(0.05)
                vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
                task.wait(0.05)
                vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
            end)
        end
end

do
    local _row2 = Instance.new("Frame", PagePlayer)
    _row2.Size                   = UDim2.new(0, 530, 0, 36)
    _row2.BackgroundTransparency = 1
    _row2.LayoutOrder            = -3
    local _rl = Instance.new("UIListLayout", _row2)
    _rl.FillDirection       = Enum.FillDirection.Horizontal
    _rl.HorizontalAlignment = Enum.HorizontalAlignment.Center
    _rl.Padding             = UDim.new(0, 10)
    _rl.SortOrder           = Enum.SortOrder.LayoutOrder

        do
            local _b = Instance.new("TextButton", _row2)
            _b.Size             = UDim2.new(0, 260, 1, 0)
            _b.BackgroundColor3 = Color3.fromRGB(20, 90, 160)
            _b.Text             = "👻 Invisible"
            _b.TextColor3       = Color3.fromRGB(255, 255, 255)
            _b.TextSize         = 12
            _b.Font             = Enum.Font.GothamBold
            _b.BorderSizePixel  = 0
            Instance.new("UICorner", _b).CornerRadius = UDim.new(0, 8)
            _b.MouseButton1Click:Connect(function()
                local vim = game:GetService("VirtualInputManager")
                local UIS = game:GetService("UserInputService")
                TweenService:Create(_b, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(70, 40, 160)}):Play()
                task.delay(0.15, function()
                    TweenService:Create(_b, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(20, 90, 160)}):Play()
                end)
                vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
                task.wait(0.2)
                local cmdBox = UIS:GetFocusedTextBox()
                if cmdBox then
                    cmdBox.Text = cmdBox.Text .. "invisible"
                    cmdBox.CursorPosition = #cmdBox.Text + 1
                end
                task.wait(0.05)
                vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
                task.wait(0.05)
                vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
            end)
        end

        do
            local _b = Instance.new("TextButton", _row2)
            _b.Size             = UDim2.new(0, 260, 1, 0)
            _b.BackgroundColor3 = Color3.fromRGB(20, 90, 160)
            _b.Text             = "👁️ Uninvisible"
            _b.TextColor3       = Color3.fromRGB(255, 255, 255)
            _b.TextSize         = 12
            _b.Font             = Enum.Font.GothamBold
            _b.BorderSizePixel  = 0
            Instance.new("UICorner", _b).CornerRadius = UDim.new(0, 8)
            _b.MouseButton1Click:Connect(function()
                local vim = game:GetService("VirtualInputManager")
                local UIS = game:GetService("UserInputService")
                TweenService:Create(_b, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(70, 40, 160)}):Play()
                task.delay(0.15, function()
                    TweenService:Create(_b, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(20, 90, 160)}):Play()
                end)
                vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
                task.wait(0.2)
                local cmdBox = UIS:GetFocusedTextBox()
                if cmdBox then
                    cmdBox.Text = cmdBox.Text .. "uninvisible"
                    cmdBox.CursorPosition = #cmdBox.Text + 1
                end
                task.wait(0.05)
                vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
                task.wait(0.05)
                vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
            end)
        end
end

MakeSection(PagePlayer, "  🧍  الشخصية")

MakeSection(PagePlayer, "  🏃  الحركة")

local _currentSpeed = 150
MakeSlider(PagePlayer, "السرعة  (WalkSpeed)", 0, 300, 150, function(v)
    _currentSpeed = v
    local h = GetHum()
    if h then h.WalkSpeed = v end
end)

local _currentJump = 80
MakeSlider(PagePlayer, "قوة القفز  (JumpPower)", 0, 300, 80, function(v)
    _currentJump = v
    local h = GetHum()
    if h then h.JumpPower = v end
end)

local _currentGravity = 150
MakeSlider(PagePlayer, "الجاذبية  (Gravity)", 0, 300, 150, function(v)
    _currentGravity = v
    workspace.Gravity = v
end)

MakeSection(PagePlayer, "  ⚡  الميزات")

local InfJumpActive = true
UserInputService.JumpRequest:Connect(function()
    if InfJumpActive then
        local h = GetHum()
        if h then h:ChangeState(Enum.HumanoidStateType.Jumping) end
    end
end)
MakeToggle(PagePlayer, "🔄  قفز لا نهائي", true, function(s)
    InfJumpActive = s
end)

local GodActive = true
local GodConn
local function SetGod(state)
    if GodConn then GodConn:Disconnect() end
    if state then
        GodConn = RunService.Heartbeat:Connect(function()
            local h = GetHum()
            if h and h.Health < h.MaxHealth then h.Health = h.MaxHealth end
        end)
    end
end
SetGod(true)
MakeToggle(PagePlayer, "🛡️  God Mode (لا تموت)", true, function(s)
    SetGod(s)
end)

local FlyActive = false
local FlyConn
local FlyBV, FlyBG
local function SetFly(state)
    FlyActive = state
    local root = GetRoot()
    if state and root then
        FlyBV = Instance.new("BodyVelocity", root)
        FlyBV.Velocity  = Vector3.zero
        FlyBV.MaxForce  = Vector3.new(1e9,1e9,1e9)
        FlyBG = Instance.new("BodyGyro", root)
        FlyBG.MaxTorque = Vector3.new(1e9,1e9,1e9)
        FlyBG.CFrame    = root.CFrame
        local cam = workspace.CurrentCamera
        local spd = 60
        FlyConn = RunService.Heartbeat:Connect(function()
            if not FlyActive then return end
            local d = Vector3.zero
            if UserInputService:IsKeyDown(Enum.KeyCode.W) then d=d+cam.CFrame.LookVector end
            if UserInputService:IsKeyDown(Enum.KeyCode.S) then d=d-cam.CFrame.LookVector end
            if UserInputService:IsKeyDown(Enum.KeyCode.A) then d=d-cam.CFrame.RightVector end
            if UserInputService:IsKeyDown(Enum.KeyCode.D) then d=d+cam.CFrame.RightVector end
            if UserInputService:IsKeyDown(Enum.KeyCode.Space) then d=d+Vector3.new(0,1,0) end
            if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) then d=d-Vector3.new(0,1,0) end
            FlyBV.Velocity = d.Magnitude>0 and d.Unit*spd or Vector3.zero
            FlyBG.CFrame   = cam.CFrame
        end)
    else
        if FlyConn then FlyConn:Disconnect() end
        if FlyBV then FlyBV:Destroy() end
        if FlyBG then FlyBG:Destroy() end
    end
end
MakeToggle(PagePlayer, "🕊️  الطيران", false, function(s)
    SetFly(s)
end)

local NoclipActive = false
local NoclipConn
MakeToggle(PagePlayer, "👻  Noclip (عبر الجدران)", true, function(s)
    NoclipActive = s
    if s then
        NoclipConn = RunService.Stepped:Connect(function()
            if not NoclipActive then return end
            local c = GetChar()
            if c then
                for _,p in pairs(c:GetDescendants()) do
                    if p:IsA("BasePart") then p.CanCollide = false end
                end
            end
        end)
    else
        if NoclipConn then NoclipConn:Disconnect() end
    end
end)

local VCS = game:GetService("VirtualUser")
game:GetService("Players").LocalPlayer.Idled:Connect(function()
    VCS:Button2Down(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
    task.wait(1)
    VCS:Button2Up(Vector2.new(0,0), workspace.CurrentCamera.CFrame)
end)
MakeToggle(PagePlayer, "💤  Anti-AFK (لا تُطرد)", true, function(_) end)

MakeSection(PagePlayer, "  👁️  ESP")

local ESP = {
    Active   = true,
    Name     = true,
    Box      = false,
    Health   = false,
    Skeleton = false,
    Line     = false,
    Distance = false,
}
local ESPFolder = Instance.new("Folder", game.CoreGui)
ESPFolder.Name  = "EliteESP"

local function BuildESP(p)
    if p == LocalPlayer then return end
    local old = ESPFolder:FindFirstChild(p.Name.."_ESP")
    if old then old:Destroy() end

    local holder = Instance.new("Folder", ESPFolder)
    holder.Name = p.Name.."_ESP"

    local BB = Instance.new("BillboardGui", holder)
    BB.Name        = "BB"
    BB.Size        = UDim2.new(0, 180, 0, 50)
    BB.StudsOffset = Vector3.new(0, 0.8, 0)
    BB.AlwaysOnTop = true

    local NameLbl = Instance.new("TextLabel", BB)
    NameLbl.Name               = "NameLbl"
    NameLbl.Size               = UDim2.new(0.5, 0, 0.22, 0)
    NameLbl.Position           = UDim2.new(0.25, 0, 0, 0)
    NameLbl.BackgroundTransparency = 1
    NameLbl.TextColor3         = Color3.fromRGB(255, 30, 30)
    NameLbl.TextStrokeColor3   = Color3.fromRGB(255, 255, 255)
    NameLbl.TextStrokeTransparency = 0.3
    NameLbl.TextScaled         = true
    NameLbl.Font               = Enum.Font.GothamBold
    NameLbl.Text               = p.Name

    local DistLbl = Instance.new("TextLabel", BB)
    DistLbl.Name               = "DistLbl"
    DistLbl.Size               = UDim2.new(1, 0, 0.45, 0)
    DistLbl.Position           = UDim2.new(0, 0, 0.55, 0)
    DistLbl.BackgroundTransparency = 1
    DistLbl.TextColor3         = Color3.fromRGB(180, 180, 255)
    DistLbl.TextScaled         = true
    DistLbl.Font               = Enum.Font.Gotham
    DistLbl.Text               = "0m"

    local HBGui = Instance.new("BillboardGui", holder)
    HBGui.Name        = "HBGui"
    HBGui.Size        = UDim2.new(0, 6, 0, 56)
    HBGui.StudsOffset = Vector3.new(-2.5, 0, 0)
    HBGui.AlwaysOnTop = true

    local HBBack = Instance.new("Frame", HBGui)
    HBBack.Size              = UDim2.new(1, 0, 1, 0)
    HBBack.BackgroundColor3  = Color3.fromRGB(20, 20, 20)
    HBBack.BorderSizePixel   = 0
    Instance.new("UICorner", HBBack).CornerRadius = UDim.new(0, 2)

    local HBFill = Instance.new("Frame", HBBack)
    HBFill.Name              = "Fill"
    HBFill.Size              = UDim2.new(1, 0, 1, 0)
    HBFill.AnchorPoint       = Vector2.new(0, 1)
    HBFill.Position          = UDim2.new(0, 0, 1, 0)
    HBFill.BackgroundColor3  = Color3.fromRGB(50, 220, 80)
    HBFill.BorderSizePixel   = 0
    Instance.new("UICorner", HBFill).CornerRadius = UDim.new(0, 2)

    local SelBox = Instance.new("SelectionBox", holder)
    SelBox.Name            = "SelBox"
    SelBox.Color3          = Color3.fromRGB(255, 50, 50)
    SelBox.LineThickness   = 0.04
    SelBox.SurfaceTransparency = 1

    local LineDraw = Drawing and Drawing.new("Line") or nil
    if LineDraw then
        LineDraw.Visible   = false
        LineDraw.Color     = Color3.fromRGB(255, 50, 50)
        LineDraw.Thickness = 1
    end

    local SkelLines = {}
    local JOINTS = {
        {"Head","UpperTorso"},{"UpperTorso","LowerTorso"},
        {"UpperTorso","LeftUpperArm"},{"LeftUpperArm","LeftLowerArm"},{"LeftLowerArm","LeftHand"},
        {"UpperTorso","RightUpperArm"},{"RightUpperArm","RightLowerArm"},{"RightLowerArm","RightHand"},
        {"LowerTorso","LeftUpperLeg"},{"LeftUpperLeg","LeftLowerLeg"},{"LeftLowerLeg","LeftFoot"},
        {"LowerTorso","RightUpperLeg"},{"RightUpperLeg","RightLowerLeg"},{"RightLowerLeg","RightFoot"},
    }
    if Drawing then
        for _ = 1, #JOINTS do
            local l = Drawing.new("Line")
            l.Visible   = false
            l.Color     = Color3.fromRGB(255, 200, 0)
            l.Thickness = 1
            table.insert(SkelLines, l)
        end
    end

    local cam = workspace.CurrentCamera

    RunService.Heartbeat:Connect(function()
        if not ESP.Active then
            BB.Enabled  = false
            HBGui.Enabled = false
            SelBox.Adornee = nil
            if LineDraw then LineDraw.Visible = false end
            for _, l in pairs(SkelLines) do l.Visible = false end
            return
        end

        local c = p.Character
        local hrp = c and c:FindFirstChild("HumanoidRootPart")
        local hum = c and c:FindFirstChildOfClass("Humanoid")
        if not hrp or not hum then
            BB.Enabled = false
            HBGui.Enabled = false
            SelBox.Adornee = nil
            if LineDraw then LineDraw.Visible = false end
            for _, l in pairs(SkelLines) do l.Visible = false end
            return
        end

        local myRoot = GetRoot()
        local dist   = myRoot and math.floor((myRoot.Position - hrp.Position).Magnitude) or 0

        BB.Adornee  = hrp
        BB.Enabled  = true
        NameLbl.Visible = ESP.Name
        NameLbl.Text    = p.Name

        DistLbl.Visible = ESP.Distance
        DistLbl.Text    = "["..dist.."m]"

        HBGui.Adornee = hrp
        HBGui.Enabled = ESP.Health
        local pct = math.clamp(hum.Health / math.max(hum.MaxHealth, 1), 0, 1)
        HBFill.Size  = UDim2.new(1, 0, pct, 0)
        HBFill.BackgroundColor3 = Color3.fromRGB(
            math.floor((1 - pct) * 255),
            math.floor(pct * 220),
            40
        )

        SelBox.Adornee = ESP.Box and hrp or nil

        if LineDraw then
            local vp = cam.ViewportSize
            local screenPos, onScreen = cam:WorldToViewportPoint(hrp.Position)
            LineDraw.Visible = ESP.Line and onScreen
            if ESP.Line and onScreen then
                LineDraw.From = Vector2.new(vp.X / 2, vp.Y)
                LineDraw.To   = Vector2.new(screenPos.X, screenPos.Y)
            end
        end

        if Drawing and #SkelLines > 0 then
            for i, pair in ipairs(JOINTS) do
                local l = SkelLines[i]
                local partA = c:FindFirstChild(pair[1])
                local partB = c:FindFirstChild(pair[2])
                if ESP.Skeleton and partA and partB then
                    local sA, onA = cam:WorldToViewportPoint(partA.Position)
                    local sB, onB = cam:WorldToViewportPoint(partB.Position)
                    l.Visible = onA and onB
                    l.From    = Vector2.new(sA.X, sA.Y)
                    l.To      = Vector2.new(sB.X, sB.Y)
                else
                    l.Visible = false
                end
            end
        end
    end)
end

Players.PlayerAdded:Connect(function(p)
    if ESP.Active then BuildESP(p) end
end)
Players.PlayerRemoving:Connect(function(p)
    local h = ESPFolder:FindFirstChild(p.Name.."_ESP")
    if h then h:Destroy() end
end)

MakeToggle(PagePlayer, "🔴  تفعيل ESP الكامل", true, function(s)
    ESP.Active = s
    if s then
        for _, p in pairs(Players:GetPlayers()) do BuildESP(p) end
    else
        for _, v in pairs(ESPFolder:GetChildren()) do v:Destroy() end
    end
end)

MakeSection(PagePlayer, "  🎛️  إعدادات ESP")

MakeToggle(PagePlayer, "👤  اسم اللاعب", true, function(s)
    ESP.Name = s
end)
MakeToggle(PagePlayer, "📏  المسافة", false, function(s)
    ESP.Distance = s
end)
MakeToggle(PagePlayer, "❤️  شريط الهلث", true, function(s)
    ESP.Health = s
end)
MakeToggle(PagePlayer, "🟥  البوكس (Box)", false, function(s)
    ESP.Box = s
end)
MakeToggle(PagePlayer, "🦴  السكيلتون", false, function(s)
    ESP.Skeleton = s
end)
MakeToggle(PagePlayer, "📍  اللاين (Line)", false, function(s)
    ESP.Line = s
end)

local TeleportService = game:GetService("TeleportService")

local SV_ACCENT = Color3.fromRGB(100, 60, 220)
local SV_CARD   = Color3.fromRGB(28,  28,  42)
local SV_PANEL  = Color3.fromRGB(22,  22,  32)
local SV_TEXT   = Color3.fromRGB(230, 230, 255)
local SV_SUB    = Color3.fromRGB(150, 150, 180)
local SV_GREEN  = Color3.fromRGB(50,  210, 100)
local SV_RED    = Color3.fromRGB(210,  55,  55)
local SV_YELLOW = Color3.fromRGB(255, 200,  50)
local SV_BLUE   = Color3.fromRGB(50,  130, 255)
local SV_TEAL   = Color3.fromRGB(40,  200, 180)
local SV_GOLD   = Color3.fromRGB(255, 185,  30)
local SV_COPY   = Color3.fromRGB(40,  180, 140)
local SV_BORDER = Color3.fromRGB(55,  55,  80)

local function sv_corner(p, r)
    Instance.new("UICorner", p).CornerRadius = UDim.new(0, r or 8)
end
local function sv_stroke(p, col, th)
    local s = Instance.new("UIStroke", p)
    s.Color = col
    s.Thickness = th or 1
end
local function sv_tw(o, props, t)
    TweenService:Create(o, TweenInfo.new(t or 0.18), props):Play()
end

local SC = Instance.new("Frame", PageNetwork)
SC.Size             = UDim2.new(1, -10, 0, 560)
SC.BackgroundTransparency = 1
SC.BorderSizePixel  = 0

local SCList = Instance.new("UIListLayout", SC)
SCList.SortOrder  = Enum.SortOrder.LayoutOrder
SCList.Padding    = UDim.new(0, 8)
local SCPad2 = Instance.new("UIPadding", SC)
SCPad2.PaddingTop   = UDim.new(0, 8)
SCPad2.PaddingLeft  = UDim.new(0, 2)
SCPad2.PaddingRight = UDim.new(0, 2)

local InfoCard2 = Instance.new("Frame", SC)
InfoCard2.Size             = UDim2.new(1, 0, 0, 120)
InfoCard2.BackgroundColor3 = SV_CARD
InfoCard2.BorderSizePixel  = 0
InfoCard2.LayoutOrder      = 1
sv_corner(InfoCard2, 10)
sv_stroke(InfoCard2, SV_ACCENT, 1.5)

local ICHead = Instance.new("Frame", InfoCard2)
ICHead.Size             = UDim2.new(1, 0, 0, 28)
ICHead.BackgroundColor3 = Color3.fromRGB(20, 14, 40)
ICHead.BorderSizePixel  = 0
sv_corner(ICHead, 10)

local ICFix = Instance.new("Frame", ICHead)
ICFix.Size             = UDim2.new(1, 0, 0.5, 0)
ICFix.Position         = UDim2.new(0, 0, 0.5, 0)
ICFix.BackgroundColor3 = Color3.fromRGB(20, 14, 40)
ICFix.BorderSizePixel  = 0

local ICHeadLbl = Instance.new("TextLabel", ICHead)
ICHeadLbl.Size                = UDim2.new(1, -20, 1, 0)
ICHeadLbl.Position            = UDim2.new(0, 12, 0, 0)
ICHeadLbl.BackgroundTransparency = 1
ICHeadLbl.Text                = "📡  السيرفر الحالي"
ICHeadLbl.TextColor3          = SV_TEXT
ICHeadLbl.TextSize            = 12
ICHeadLbl.Font                = Enum.Font.GothamBold
ICHeadLbl.TextXAlignment      = Enum.TextXAlignment.Left

local Dot2 = Instance.new("Frame", ICHead)
Dot2.Size             = UDim2.new(0, 8, 0, 8)
Dot2.Position         = UDim2.new(1, -16, 0.5, -4)
Dot2.BackgroundColor3 = SV_GREEN
Dot2.BorderSizePixel  = 0
sv_corner(Dot2, 8)

local function makeRow(yOff, label, val, valCol)
    local R = Instance.new("Frame", InfoCard2)
    R.Size               = UDim2.new(1, -16, 0, 18)
    R.Position           = UDim2.new(0, 8, 0, yOff)
    R.BackgroundTransparency = 1
    R.BorderSizePixel    = 0

    local L1 = Instance.new("TextLabel", R)
    L1.Size              = UDim2.new(0.38, 0, 1, 0)
    L1.BackgroundTransparency = 1
    L1.Text              = label
    L1.TextColor3        = SV_SUB
    L1.TextSize          = 10
    L1.Font              = Enum.Font.Gotham
    L1.TextXAlignment    = Enum.TextXAlignment.Left

    local L2 = Instance.new("TextLabel", R)
    L2.Size              = UDim2.new(0.62, 0, 1, 0)
    L2.Position          = UDim2.new(0.38, 0, 0, 0)
    L2.BackgroundTransparency = 1
    L2.Text              = val
    L2.TextColor3        = valCol or SV_TEXT
    L2.TextSize          = 10
    L2.Font              = Enum.Font.GothamBold
    L2.TextXAlignment    = Enum.TextXAlignment.Left
    L2.TextTruncate      = Enum.TextTruncate.AtEnd
    return L2
end

local RowPlaceId  = makeRow(32, "🆔 Place ID:", tostring(game.PlaceId), SV_TEAL)
local RowJobId    = makeRow(50, "🔑 Job ID:",   game.JobId:sub(1, 24), SV_BLUE)
local RowPlayers  = makeRow(68, "👥 اللاعبون:", "#Players", SV_GREEN)
local RowMapName  = makeRow(88, "🗺️ الخريطة:", "جارٍ...", SV_YELLOW)

task.spawn(function()
    while InfoCard2 and InfoCard2.Parent do
        pcall(function()
            RowPlayers.Text = tostring(#Players:GetPlayers()) .. " / " .. Players.MaxPlayers
        end)
        task.wait(5)
    end
end)

task.spawn(function()
    local ok, res = pcall(function()
        return game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId)
    end)
    if ok and res and res.Name then
        RowMapName.Text = res.Name
    else
        RowMapName.Text = tostring(game.PlaceId)
    end
end)

local CopyJBtn = Instance.new("TextButton", InfoCard2)
CopyJBtn.Size             = UDim2.new(0, 80, 0, 16)
CopyJBtn.Position         = UDim2.new(1, -86, 0, 50)
CopyJBtn.BackgroundColor3 = SV_COPY
CopyJBtn.Text             = "📋 نسخ"
CopyJBtn.TextColor3       = Color3.fromRGB(10, 10, 10)
CopyJBtn.TextSize         = 9
CopyJBtn.Font             = Enum.Font.GothamBold
CopyJBtn.BorderSizePixel  = 0
sv_corner(CopyJBtn, 5)
CopyJBtn.MouseButton1Click:Connect(function()
    pcall(function()
        if setclipboard then
            setclipboard(game.JobId)
        end
    end)
    CopyJBtn.Text = "✔ نُسخ!"
    sv_tw(CopyJBtn, {BackgroundColor3 = SV_GREEN})
    task.delay(1.5, function()
        if CopyJBtn and CopyJBtn.Parent then
            CopyJBtn.Text = "📋 نسخ"
            sv_tw(CopyJBtn, {BackgroundColor3 = SV_COPY})
        end
    end)
end)

local RJCard2 = Instance.new("Frame", SC)
RJCard2.Size             = UDim2.new(1, 0, 0, 80)
RJCard2.BackgroundColor3 = SV_CARD
RJCard2.BorderSizePixel  = 0
RJCard2.LayoutOrder      = 2
sv_corner(RJCard2, 10)
sv_stroke(RJCard2, SV_BORDER, 1)

local RJLbl = Instance.new("TextLabel", RJCard2)
RJLbl.Size               = UDim2.new(1, -20, 0, 20)
RJLbl.Position           = UDim2.new(0, 12, 0, 6)
RJLbl.BackgroundTransparency = 1
RJLbl.Text               = "🔄  Re-Join"
RJLbl.TextColor3         = SV_TEXT
RJLbl.TextSize           = 13
RJLbl.Font               = Enum.Font.GothamBold
RJLbl.TextXAlignment     = Enum.TextXAlignment.Left

local RJSub2 = Instance.new("TextLabel", RJCard2)
RJSub2.Size              = UDim2.new(1, -20, 0, 14)
RJSub2.Position          = UDim2.new(0, 12, 0, 26)
RJSub2.BackgroundTransparency = 1
RJSub2.Text              = "اخرج وارجع للعبة"
RJSub2.TextColor3        = SV_SUB
RJSub2.TextSize          = 9
RJSub2.Font              = Enum.Font.Gotham
RJSub2.TextXAlignment    = Enum.TextXAlignment.Left

local RJSameBtn = Instance.new("TextButton", RJCard2)
RJSameBtn.Size             = UDim2.new(0.46, 0, 0, 30)
RJSameBtn.Position         = UDim2.new(0.52, 0, 1, -38)
RJSameBtn.BackgroundColor3 = SV_ACCENT
RJSameBtn.Text             = "🔁 نفس السيرفر"
RJSameBtn.TextColor3       = SV_TEXT
RJSameBtn.TextSize         = 11
RJSameBtn.Font             = Enum.Font.GothamBold
RJSameBtn.BorderSizePixel  = 0
sv_corner(RJSameBtn, 7)
RJSameBtn.MouseButton1Click:Connect(function()
    local pid = game.PlaceId
    local jid = game.JobId
    pcall(function()
        TeleportService:TeleportToPlaceInstance(pid, jid, LocalPlayer)
    end)
end)

local RJNewBtn = Instance.new("TextButton", RJCard2)
RJNewBtn.Size             = UDim2.new(0.46, 0, 0, 30)
RJNewBtn.Position         = UDim2.new(0.02, 0, 1, -38)
RJNewBtn.BackgroundColor3 = Color3.fromRGB(45, 105, 195)
RJNewBtn.Text             = "🆕 سيرفر جديد"
RJNewBtn.TextColor3       = SV_TEXT
RJNewBtn.TextSize         = 11
RJNewBtn.Font             = Enum.Font.GothamBold
RJNewBtn.BorderSizePixel  = 0
sv_corner(RJNewBtn, 7)
RJNewBtn.MouseButton1Click:Connect(function()
    local pid = game.PlaceId
    pcall(function()
        TeleportService:Teleport(pid, LocalPlayer)
    end)
end)

local SaveHeader = Instance.new("Frame", SC)
SaveHeader.Size             = UDim2.new(1, 0, 0, 34)
SaveHeader.BackgroundColor3 = Color3.fromRGB(20, 14, 40)
SaveHeader.BorderSizePixel  = 0
SaveHeader.LayoutOrder      = 3
sv_corner(SaveHeader, 8)
sv_stroke(SaveHeader, SV_ACCENT, 1)

local SaveHLbl = Instance.new("TextLabel", SaveHeader)
SaveHLbl.Size              = UDim2.new(0.5, 0, 1, 0)
SaveHLbl.Position          = UDim2.new(0, 12, 0, 0)
SaveHLbl.BackgroundTransparency = 1
SaveHLbl.Text              = "🗂️  مابات محفوظة"
SaveHLbl.TextColor3        = SV_TEXT
SaveHLbl.TextSize          = 12
SaveHLbl.Font              = Enum.Font.GothamBold
SaveHLbl.TextXAlignment    = Enum.TextXAlignment.Left

local SaveBtn2 = Instance.new("TextButton", SaveHeader)
SaveBtn2.Size              = UDim2.new(0, 130, 0, 24)
SaveBtn2.Position          = UDim2.new(1, -136, 0.5, -12)
SaveBtn2.BackgroundColor3  = SV_GOLD
SaveBtn2.Text              = "💾 احفظ الحالي"
SaveBtn2.TextColor3        = Color3.fromRGB(10, 10, 10)
SaveBtn2.TextSize          = 11
SaveBtn2.Font              = Enum.Font.GothamBold
SaveBtn2.BorderSizePixel   = 0
sv_corner(SaveBtn2, 6)

local SavedScroll = Instance.new("ScrollingFrame", SC)
SavedScroll.Size               = UDim2.new(1, 0, 0, 260)
SavedScroll.BackgroundColor3   = SV_PANEL
SavedScroll.BorderSizePixel    = 0
SavedScroll.LayoutOrder        = 4
SavedScroll.ScrollBarThickness = 4
SavedScroll.ScrollBarImageColor3 = SV_ACCENT
SavedScroll.CanvasSize         = UDim2.new(0, 0, 0, 0)
sv_corner(SavedScroll, 8)
local SSList = Instance.new("UIListLayout", SavedScroll)
SSList.SortOrder   = Enum.SortOrder.LayoutOrder
SSList.Padding     = UDim.new(0, 6)
local SSPad = Instance.new("UIPadding", SavedScroll)
SSPad.PaddingTop    = UDim.new(0, 8)
SSPad.PaddingBottom = UDim.new(0, 8)
SSPad.PaddingLeft   = UDim.new(0, 8)
SSPad.PaddingRight  = UDim.new(0, 8)

SSList:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    SavedScroll.CanvasSize = UDim2.new(0, 0, 0, SSList.AbsoluteContentSize.Y + 16)
end)

local EmptyHint = Instance.new("TextLabel", SavedScroll)
EmptyHint.Size               = UDim2.new(1, 0, 0, 40)
EmptyHint.BackgroundTransparency = 1
EmptyHint.Text               = "لا يوجد شيء  —  اضغط 💾 احفظ الحالي"
EmptyHint.TextColor3         = SV_SUB
EmptyHint.TextSize           = 11
EmptyHint.Font               = Enum.Font.Gotham
EmptyHint.TextXAlignment     = Enum.TextXAlignment.Center
EmptyHint.Visible            = true

local savedList2  = {}
local savedIdx2   = 0

local function buildCard2(entry, idx)
    EmptyHint.Visible = false
    local CC = Instance.new("Frame", SavedScroll)
    CC.Size             = UDim2.new(1, 0, 0, 80)
    CC.BackgroundColor3 = SV_CARD
    CC.BorderSizePixel  = 0
    CC.LayoutOrder      = idx
    sv_corner(CC, 8)
    sv_stroke(CC, SV_BORDER, 1)

    local Strip2 = Instance.new("Frame", CC)
    Strip2.Size             = UDim2.new(0, 3, 0.65, 0)
    Strip2.Position         = UDim2.new(0, 6, 0.17, 0)
    Strip2.BackgroundColor3 = SV_ACCENT
    Strip2.BorderSizePixel  = 0
    sv_corner(Strip2, 3)

    local NumLbl2 = Instance.new("TextLabel", CC)
    NumLbl2.Size             = UDim2.new(0, 22, 0, 22)
    NumLbl2.Position         = UDim2.new(0, 14, 0, 8)
    NumLbl2.BackgroundColor3 = SV_ACCENT
    NumLbl2.Text             = tostring(idx)
    NumLbl2.TextColor3       = SV_TEXT
    NumLbl2.TextSize         = 10
    NumLbl2.Font             = Enum.Font.GothamBold
    NumLbl2.BorderSizePixel  = 0
    sv_corner(NumLbl2, 5)

    local NameL2 = Instance.new("TextLabel", CC)
    NameL2.Size             = UDim2.new(1, -110, 0, 18)
    NameL2.Position         = UDim2.new(0, 42, 0, 6)
    NameL2.BackgroundTransparency = 1
    NameL2.Text             = entry.name
    NameL2.TextColor3       = SV_TEXT
    NameL2.TextSize         = 12
    NameL2.Font             = Enum.Font.GothamBold
    NameL2.TextXAlignment   = Enum.TextXAlignment.Left
    NameL2.TextTruncate     = Enum.TextTruncate.AtEnd

    local InfoL2 = Instance.new("TextLabel", CC)
    InfoL2.Size             = UDim2.new(1, -110, 0, 13)
    InfoL2.Position         = UDim2.new(0, 42, 0, 24)
    InfoL2.BackgroundTransparency = 1
    InfoL2.Text             = "⏱ " .. entry.time .. "   🆔 " .. tostring(entry.placeId)
    InfoL2.TextColor3       = SV_SUB
    InfoL2.TextSize         = 9
    InfoL2.Font             = Enum.Font.Gotham
    InfoL2.TextXAlignment   = Enum.TextXAlignment.Left

    local TPSameB = Instance.new("TextButton", CC)
    TPSameB.Size             = UDim2.new(0, 110, 0, 24)
    TPSameB.Position         = UDim2.new(0, 14, 0, 48)
    TPSameB.BackgroundColor3 = SV_ACCENT
    TPSameB.Text             = "🔁 نفس السيرفر"
    TPSameB.TextColor3       = SV_TEXT
    TPSameB.TextSize         = 10
    TPSameB.Font             = Enum.Font.GothamBold
    TPSameB.BorderSizePixel  = 0
    sv_corner(TPSameB, 6)
    local eJobId = entry.jobId
    local ePlaceId = entry.placeId
    TPSameB.MouseButton1Click:Connect(function()
        pcall(function()
            TeleportService:TeleportToPlaceInstance(ePlaceId, eJobId, LocalPlayer)
        end)
    end)

    local TPNewB = Instance.new("TextButton", CC)
    TPNewB.Size             = UDim2.new(0, 108, 0, 24)
    TPNewB.Position         = UDim2.new(0, 130, 0, 48)
    TPNewB.BackgroundColor3 = Color3.fromRGB(45, 105, 195)
    TPNewB.Text             = "🆕 سيرفر جديد"
    TPNewB.TextColor3       = SV_TEXT
    TPNewB.TextSize         = 10
    TPNewB.Font             = Enum.Font.GothamBold
    TPNewB.BorderSizePixel  = 0
    sv_corner(TPNewB, 6)
    TPNewB.MouseButton1Click:Connect(function()
        pcall(function()
            TeleportService:Teleport(ePlaceId, LocalPlayer)
        end)
    end)

    local DelB = Instance.new("TextButton", CC)
    DelB.Size             = UDim2.new(0, 26, 0, 24)
    DelB.Position         = UDim2.new(1, -34, 0, 48)
    DelB.BackgroundColor3 = SV_RED
    DelB.Text             = "✕"
    DelB.TextColor3       = SV_TEXT
    DelB.TextSize         = 12
    DelB.Font             = Enum.Font.GothamBold
    DelB.BorderSizePixel  = 0
    sv_corner(DelB, 6)
    DelB.MouseButton1Click:Connect(function()
        CC:Destroy()
        for k, v in ipairs(savedList2) do
            if v.jobId == eJobId then
                table.remove(savedList2, k)
                break
            end
        end
        if #savedList2 == 0 then
            EmptyHint.Visible = true
        end
    end)
end

SaveBtn2.MouseButton1Click:Connect(function()
    for _, sv2 in ipairs(savedList2) do
        if sv2.jobId == game.JobId then
            SaveBtn2.Text = "✘ محفوظ مسبقاً"
            sv_tw(SaveBtn2, {BackgroundColor3 = SV_RED})
            task.delay(1.5, function()
                if SaveBtn2 and SaveBtn2.Parent then
                    SaveBtn2.Text = "💾 احفظ الحالي"
                    sv_tw(SaveBtn2, {BackgroundColor3 = SV_GOLD})
                end
            end)
            return
        end
    end
    savedIdx2 = savedIdx2 + 1
    local entry2 = {
        placeId = game.PlaceId,
        jobId   = game.JobId,
        name    = RowMapName.Text,
        time    = os.date("%H:%M"),
    }
    table.insert(savedList2, entry2)
    buildCard2(entry2, savedIdx2)
    SaveBtn2.Text = "✔ تم الحفظ!"
    sv_tw(SaveBtn2, {BackgroundColor3 = SV_GREEN})
    task.delay(1.5, function()
        if SaveBtn2 and SaveBtn2.Parent then
            SaveBtn2.Text = "💾 احفظ الحالي"
            sv_tw(SaveBtn2, {BackgroundColor3 = SV_GOLD})
        end
    end)
end)

task.spawn(function()
    task.wait(2)
    if not (InfoCard2 and InfoCard2.Parent) then return end
    savedIdx2 = 1
    local entry2 = {
        placeId = game.PlaceId,
        jobId   = game.JobId,
        name    = RowMapName.Text,
        time    = os.date("%H:%M") .. " (الآن)",
    }
    table.insert(savedList2, entry2)
    buildCard2(entry2, savedIdx2)
end)

local dragging, dragStart, startPos
TitleBar.InputBegan:Connect(function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging  = true
        dragStart = i.Position
        startPos  = MainFrame.Position
    end
end)
TitleBar.InputEnded:Connect(function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton1 then dragging = false end
end)
UserInputService.InputChanged:Connect(function(i)
    if dragging and i.UserInputType == Enum.UserInputType.MouseMovement then
        local delta = i.Position - dragStart
        MainFrame.Position = UDim2.new(
            startPos.X.Scale, startPos.X.Offset + delta.X,
            startPos.Y.Scale, startPos.Y.Offset + delta.Y
        )
    end
end)

local MIN_HEIGHT = 300
local MAX_HEIGHT = 900

local ResizeHandle = Instance.new("Frame", MainFrame)
ResizeHandle.Size                  = UDim2.new(1, 0, 0, 8)
ResizeHandle.Position              = UDim2.new(0, 0, 1, -8)
ResizeHandle.BackgroundColor3      = Color3.fromRGB(100, 60, 220)
ResizeHandle.BackgroundTransparency = 0.65
ResizeHandle.BorderSizePixel       = 0
ResizeHandle.ZIndex                = 10
local RHCorner = Instance.new("UICorner", ResizeHandle)
RHCorner.CornerRadius = UDim.new(0, 4)

local ResizeIcon = Instance.new("TextLabel", ResizeHandle)
ResizeIcon.Size               = UDim2.new(1, 0, 1, 0)
ResizeIcon.BackgroundTransparency = 1
ResizeIcon.Text               = "— — —"
ResizeIcon.TextColor3         = Color3.fromRGB(255, 255, 255)
ResizeIcon.TextTransparency   = 0.3
ResizeIcon.TextSize           = 7
ResizeIcon.Font               = Enum.Font.GothamBold
ResizeIcon.ZIndex             = 11

ResizeHandle.MouseEnter:Connect(function()
    TweenService:Create(ResizeHandle, TweenInfo.new(0.12), {
        BackgroundTransparency = 0.1,
        BackgroundColor3       = Color3.fromRGB(130, 80, 255)
    }):Play()
end)
ResizeHandle.MouseLeave:Connect(function()
    TweenService:Create(ResizeHandle, TweenInfo.new(0.12), {
        BackgroundTransparency = 0.65,
        BackgroundColor3       = Color3.fromRGB(100, 60, 220)
    }):Play()
end)

local resizing     = false
local resizeStartY = 0
local resizeStartH = 0

ResizeHandle.InputBegan:Connect(function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton1 then
        resizing     = true
        resizeStartY = i.Position.Y
        resizeStartH = MainFrame.AbsoluteSize.Y
    end
end)

UserInputService.InputEnded:Connect(function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton1 then
        resizing = false
    end
end)

UserInputService.InputChanged:Connect(function(i)
    if resizing and i.UserInputType == Enum.UserInputType.MouseMovement then
        local delta = i.Position.Y - resizeStartY
        local newH  = math.clamp(resizeStartH + delta, MIN_HEIGHT, MAX_HEIGHT)
        MainFrame.Size = UDim2.new(0, MainFrame.AbsoluteSize.X, 0, newH)
    end
end)

local minimized = false
CloseBtn.MouseButton1Click:Connect(function()
    TweenService:Create(MainFrame, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {
        Size = UDim2.new(0, 0, 0, 0)
    }):Play()
    task.delay(0.31, function() ScreenGui:Destroy() end)
end)

MinBtn.MouseButton1Click:Connect(function()
    minimized = not minimized
    if minimized then
        TweenService:Create(MainFrame, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {
            Size = UDim2.new(0, 560, 0, 50)
        }):Play()
        MinBtn.Text = "▲"
    else
        TweenService:Create(MainFrame, TweenInfo.new(0.3, Enum.EasingStyle.Quad), {
            Size = UDim2.new(0, 560, 0, 640)
        }):Play()
        MinBtn.Text = "—"
    end
end)

MainFrame.Size = UDim2.new(0, 0, 0, 0)
TweenService:Create(MainFrame, TweenInfo.new(0.4, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
    Size = UDim2.new(0, 560, 0, 640)
}):Play()

local ToggleBtn = Instance.new("Frame")
ToggleBtn.Name              = "ToggleBtn"
ToggleBtn.Size              = UDim2.new(0, 48, 0, 48)
ToggleBtn.Position          = UDim2.new(0, 16, 0.5, -24)
ToggleBtn.BackgroundColor3  = Color3.fromRGB(100, 60, 220)
ToggleBtn.BorderSizePixel   = 0
ToggleBtn.ZIndex            = 10
ToggleBtn.Parent            = ScreenGui

local TBC = Instance.new("UICorner", ToggleBtn)
TBC.CornerRadius = UDim.new(1, 0)

local ToggleStroke = Instance.new("UIStroke", ToggleBtn)
ToggleStroke.Color     = Color3.fromRGB(180, 120, 255)
ToggleStroke.Thickness = 2
ToggleStroke.Transparency = 0.4

local ToggleIcon = Instance.new("TextLabel", ToggleBtn)
ToggleIcon.Size              = UDim2.new(1, 0, 1, 0)
ToggleIcon.BackgroundTransparency = 1
ToggleIcon.Text              = "🏠"
ToggleIcon.TextSize          = 22
ToggleIcon.Font              = Enum.Font.GothamBold
ToggleIcon.TextXAlignment    = Enum.TextXAlignment.Center
ToggleIcon.ZIndex            = 11

local pulse = true
task.spawn(function()
    while pulse do
        TweenService:Create(ToggleBtn, TweenInfo.new(0.9, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {
            BackgroundColor3 = Color3.fromRGB(130, 80, 255)
        }):Play()
        task.wait(0.9)
        TweenService:Create(ToggleBtn, TweenInfo.new(0.9, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {
            BackgroundColor3 = Color3.fromRGB(80, 40, 180)
        }):Play()
        task.wait(0.9)
    end
end)

local togDragging, togDragStart, togStartPos = false, nil, nil
local didDrag = false

ToggleBtn.InputBegan:Connect(function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton1 then
        togDragging  = true
        didDrag      = false
        togDragStart = i.Position
        togStartPos  = ToggleBtn.Position
    end
end)
ToggleBtn.InputEnded:Connect(function(i)
    if i.UserInputType == Enum.UserInputType.MouseButton1 then
        togDragging = false
        if not didDrag then
            
            local isOpen = MainFrame.Visible
            if isOpen then
                TweenService:Create(MainFrame, TweenInfo.new(0.3, Enum.EasingStyle.Quad, Enum.EasingDirection.In), {
                    Size     = UDim2.new(0, 560, 0, 0),
                    Position = MainFrame.Position + UDim2.new(0, 0, 0, 20)
                }):Play()
                task.delay(0.31, function() MainFrame.Visible = false end)
                ToggleIcon.Text = "☰"
                TweenService:Create(ToggleBtn, TweenInfo.new(0.2), {
                    BackgroundColor3 = Color3.fromRGB(60, 60, 80)
                }):Play()
                pulse = false
            else
                MainFrame.Visible = true
                MainFrame.Size    = UDim2.new(0, 560, 0, 0)
                MainFrame.Position = MainFrame.Position - UDim2.new(0, 0, 0, 20)
                TweenService:Create(MainFrame, TweenInfo.new(0.4, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
                    Size     = UDim2.new(0, 560, 0, 640),
                    Position = MainFrame.Position + UDim2.new(0, 0, 0, 20)
                }):Play()
                ToggleIcon.Text = "🏠"
                pulse = true
                task.spawn(function()
                    while pulse do
                        TweenService:Create(ToggleBtn, TweenInfo.new(0.9, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {
                            BackgroundColor3 = Color3.fromRGB(130, 80, 255)
                        }):Play()
                        task.wait(0.9)
                        TweenService:Create(ToggleBtn, TweenInfo.new(0.9, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {
                            BackgroundColor3 = Color3.fromRGB(80, 40, 180)
                        }):Play()
                        task.wait(0.9)
                    end
                end)
            end
        end
    end
end)
UserInputService.InputChanged:Connect(function(i)
    if togDragging and i.UserInputType == Enum.UserInputType.MouseMovement then
        local delta = i.Position - togDragStart
        if delta.Magnitude > 4 then didDrag = true end
        ToggleBtn.Position = UDim2.new(
            togStartPos.X.Scale, togStartPos.X.Offset + delta.X,
            togStartPos.Y.Scale, togStartPos.Y.Offset + delta.Y
        )
    end
end)

UserInputService.InputBegan:Connect(function(i, gpe)
    if gpe then return end
    if i.KeyCode == Enum.KeyCode.RightShift then
        MainFrame.Visible = not MainFrame.Visible
    end
end)

local SCRIPTS = {
    {
        name  = "Pastefy Script",
        desc  = "fnEwkJlo",
        url   = "https://pastefy.app/fnEwkJlo/raw",
        color = Color3.fromRGB(100, 60, 220),
        icon  = "📄",
    },
    {
        name  = "MUTAGEN Troller",
        desc  = "Universal Troller Script",
        url   = "https://rawscripts.net/raw/Universal-Script-MUTAGEN-Universall-Troller-script-180715",
        color = Color3.fromRGB(180, 40, 40),
        icon  = "💀",
    },
    {
        name  = "Emote",
        desc  = "Emotes Script",
        url   = "https://raw.githubusercontent.com/7yd7/Hub/refs/heads/Branch/GUIS/Emotes.lua",
        color = Color3.fromRGB(255, 140, 0),
        icon  = "🕺",
    },
    {
        name  = "الحماية",
        desc  = "الحماية",
        code  = [==[
-- Coordinates HUD + RESPAWN + AUTO RESPAWN
-- LocalScript في StarterPlayerScripts
local Players      = game:GetService("Players")
local RunService   = game:GetService("RunService")
local VIM          = game:GetService("VirtualInputManager")
local UIS          = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local player       = Players.LocalPlayer
local playerGui    = player:WaitForChild("PlayerGui")

-- === GUI Setup ===
local screenGui = Instance.new("ScreenGui")
screenGui.Name           = "CoordsHUD"
screenGui.ResetOnSpawn   = false
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.Parent         = playerGui

local frame = Instance.new("Frame")
frame.Size                   = UDim2.new(0, 220, 0, 237)  -- أكبر عشان 4 أزرار
frame.Position               = UDim2.new(0, 16, 1, -253)
frame.BackgroundColor3       = Color3.fromRGB(15, 15, 15)
frame.BackgroundTransparency = 0.3
frame.BorderSizePixel        = 0
frame.Parent                 = screenGui

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 8)
corner.Parent       = frame

local stroke = Instance.new("UIStroke")
stroke.Color        = Color3.fromRGB(0, 200, 255)
stroke.Thickness    = 1.5
stroke.Transparency = 0.4
stroke.Parent       = frame

local title = Instance.new("TextLabel")
title.Size               = UDim2.new(1, 0, 0, 24)
title.Position           = UDim2.new(0, 0, 0, 4)
title.BackgroundTransparency = 1
title.Text               = "📍 COORDINATES"
title.TextColor3         = Color3.fromRGB(0, 200, 255)
title.TextSize           = 13
title.Font               = Enum.Font.GothamBold
title.Parent             = frame

local coordsLabel = Instance.new("TextLabel")
coordsLabel.Size                 = UDim2.new(1, -16, 0, 56)
coordsLabel.Position             = UDim2.new(0, 8, 0, 28)
coordsLabel.BackgroundTransparency = 1
coordsLabel.TextColor3           = Color3.fromRGB(220, 220, 220)
coordsLabel.TextSize             = 13
coordsLabel.Font                 = Enum.Font.GothamMedium
coordsLabel.TextXAlignment       = Enum.TextXAlignment.Left
coordsLabel.TextYAlignment       = Enum.TextYAlignment.Top
coordsLabel.Parent               = frame

-- === RESPAWN Button ===
local resButton = Instance.new("TextButton")
resButton.Size             = UDim2.new(1, -16, 0, 28)
resButton.Position         = UDim2.new(0, 8, 0, 89)
resButton.BackgroundColor3 = Color3.fromRGB(200, 40, 40)
resButton.BorderSizePixel  = 0
resButton.Text             = "🔄 Respawn"
resButton.TextColor3       = Color3.fromRGB(255, 255, 255)
resButton.TextSize         = 13
resButton.Font             = Enum.Font.GothamBold
resButton.Parent           = frame

Instance.new("UICorner", resButton).CornerRadius = UDim.new(0, 6)

resButton.MouseEnter:Connect(function()
    resButton.BackgroundColor3 = Color3.fromRGB(230, 60, 60)
end)
resButton.MouseLeave:Connect(function()
    resButton.BackgroundColor3 = Color3.fromRGB(200, 40, 40)
end)

-- === RESPAWN Logic (طريقة Char) ===
local savedCFrame = nil  -- آخر موقع قبل الـ res

local function sendRes()
    VIM:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
    VIM:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
    task.wait(0.2)
    local cmdBox = UIS:GetFocusedTextBox()
    if cmdBox then
        cmdBox.Text = cmdBox.Text .. "res"
        cmdBox.CursorPosition = #cmdBox.Text + 1
    end
    task.wait(0.05)
    VIM:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
    VIM:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
    task.wait(0.05)
    VIM:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
    VIM:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
end

-- يحفظ الموقع → يرسل res → ينتظر الـ respawn → يرجع للموقع
local function sendResAndReturn()
    local char = player.Character
    if char then
        local root = char:FindFirstChild("HumanoidRootPart")
        if root then
            savedCFrame = root.CFrame  -- حفظ الموقع + الاتجاه
        end
    end

    sendRes()

    if savedCFrame then
        local newChar = player.CharacterAdded:Wait()
        local newRoot = newChar:WaitForChild("HumanoidRootPart", 10)
        if newRoot then
            task.wait(0.15)  -- انتظر الـ physics تستقر
            newRoot.CFrame = savedCFrame
        end
    end
end

resButton.MouseButton1Click:Connect(function()
    TweenService:Create(resButton, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(255, 100, 100)}):Play()
    task.delay(0.15, function()
        TweenService:Create(resButton, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(200, 40, 40)}):Play()
    end)
    task.spawn(sendResAndReturn)
end)

-- === KEYBIND Button ===
local boundKey    = nil   -- الكي المحفوظ
local listenMode  = false -- وضع الاستماع

local keyBindButton = Instance.new("TextButton")
keyBindButton.Size             = UDim2.new(1, -16, 0, 28)
keyBindButton.Position         = UDim2.new(0, 8, 0, 126)
keyBindButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
keyBindButton.BorderSizePixel  = 0
keyBindButton.Text             = "⌨ Bind Key: None"
keyBindButton.TextColor3       = Color3.fromRGB(200, 200, 200)
keyBindButton.TextSize         = 12
keyBindButton.Font             = Enum.Font.GothamMedium
keyBindButton.Parent           = frame

Instance.new("UICorner", keyBindButton).CornerRadius = UDim.new(0, 6)

local keyStroke = Instance.new("UIStroke")
keyStroke.Color        = Color3.fromRGB(100, 100, 100)
keyStroke.Thickness    = 1
keyStroke.Parent       = keyBindButton

keyBindButton.MouseButton1Click:Connect(function()
    listenMode = true
    keyBindButton.Text             = "🔴 Press any key..."
    keyBindButton.BackgroundColor3 = Color3.fromRGB(60, 20, 20)
    keyStroke.Color                = Color3.fromRGB(255, 60, 60)
end)

UIS.InputBegan:Connect(function(input, gameProcessed)
    -- وضع الاستماع: حفظ الكي
    if listenMode and input.UserInputType == Enum.UserInputType.Keyboard then
        listenMode = false
        boundKey   = input.KeyCode
        keyBindButton.Text             = "⌨ Bind: " .. tostring(input.KeyCode.Name)
        keyBindButton.BackgroundColor3 = Color3.fromRGB(20, 80, 20)
        keyStroke.Color                = Color3.fromRGB(60, 200, 60)
        return
    end
    -- تشغيل Respawn بالكي المحفوظ
    if not gameProcessed and boundKey and input.KeyCode == boundKey then
        task.spawn(sendResAndReturn)
    end
end)

-- === AUTO RESPAWN Button ===
local autoButton = Instance.new("TextButton")
autoButton.Size             = UDim2.new(1, -16, 0, 28)
autoButton.Position         = UDim2.new(0, 8, 0, 163)  -- تحت الـ Keybind
autoButton.BackgroundColor3 = Color3.fromRGB(120, 40, 200)
autoButton.BorderSizePixel  = 0
autoButton.Text             = "♾ Auto Respawn"
autoButton.TextColor3       = Color3.fromRGB(255, 255, 255)
autoButton.TextSize         = 13
autoButton.Font             = Enum.Font.GothamBold
autoButton.Parent           = frame

Instance.new("UICorner", autoButton).CornerRadius = UDim.new(0, 6)

autoButton.MouseEnter:Connect(function()
    if not autoButton:GetAttribute("Active") then
        autoButton.BackgroundColor3 = Color3.fromRGB(150, 60, 230)
    end
end)
autoButton.MouseLeave:Connect(function()
    if not autoButton:GetAttribute("Active") then
        autoButton.BackgroundColor3 = Color3.fromRGB(120, 40, 200)
    end
end)

-- === AUTO RESPAWN Logic ===
local autoActive = false

autoButton.MouseButton1Click:Connect(function()
    autoActive = not autoActive

    if autoActive then
        -- شغّل
        autoButton:SetAttribute("Active", true)
        autoButton.Text             = "⏹ Stop Auto"
        autoButton.BackgroundColor3 = Color3.fromRGB(40, 160, 40)

        task.spawn(function()
            while autoActive do
                sendResAndReturn()
                task.wait(0.7)  -- انتظر 0.7 ثانية بين كل res
            end
        end)
    else
        -- وقّف
        autoButton:SetAttribute("Active", false)
        autoButton.Text             = "♾ Auto Respawn"
        autoButton.BackgroundColor3 = Color3.fromRGB(120, 40, 200)
    end
end)

-- === TELEPORT TO SPOT Button ===
local SPOT = Vector3.new(-45.2, -504.5, 97.3)  -- الاحداثية الثابتة
local spotSavedCFrame = nil  -- الموقع اللي كان فيه قبل الـ TP
local atSpot = false

local spotButton = Instance.new("TextButton")
spotButton.Size             = UDim2.new(1, -16, 0, 28)
spotButton.Position         = UDim2.new(0, 8, 0, 200)
spotButton.BackgroundColor3 = Color3.fromRGB(20, 120, 60)
spotButton.BorderSizePixel  = 0
spotButton.Text             = "📍 Go to Spot"
spotButton.TextColor3       = Color3.fromRGB(255, 255, 255)
spotButton.TextSize         = 12
spotButton.Font             = Enum.Font.GothamBold
spotButton.Parent           = frame

Instance.new("UICorner", spotButton).CornerRadius = UDim.new(0, 6)

spotButton.MouseEnter:Connect(function()
    if not atSpot then
        spotButton.BackgroundColor3 = Color3.fromRGB(30, 160, 80)
    else
        spotButton.BackgroundColor3 = Color3.fromRGB(160, 100, 20)
    end
end)
spotButton.MouseLeave:Connect(function()
    if not atSpot then
        spotButton.BackgroundColor3 = Color3.fromRGB(20, 120, 60)
    else
        spotButton.BackgroundColor3 = Color3.fromRGB(120, 70, 10)
    end
end)

spotButton.MouseButton1Click:Connect(function()
    local char = player.Character
    if not char then return end
    local root = char:FindFirstChild("HumanoidRootPart")
    if not root then return end

    TweenService:Create(spotButton, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(255, 255, 100)}):Play()

    if not atSpot then
        -- حفظ الموقع الحالي والتيلبورت للسبوت
        spotSavedCFrame = root.CFrame
        root.CFrame = CFrame.new(SPOT)
        atSpot = true
        task.delay(0.12, function()
            TweenService:Create(spotButton, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(120, 70, 10)}):Play()
        end)
        spotButton.Text = "↩ Return"
    else
        -- رجوع للموقع المحفوظ
        if spotSavedCFrame then
            root.CFrame = spotSavedCFrame
        end
        atSpot = false
        task.delay(0.12, function()
            TweenService:Create(spotButton, TweenInfo.new(0.1), {BackgroundColor3 = Color3.fromRGB(20, 120, 60)}):Play()
        end)
        spotButton.Text = "📍 Go to Spot"
        spotSavedCFrame = nil
    end
end)

-- إذا مات/ريسبون يتريسيت الحالة
player.CharacterAdded:Connect(function()
    atSpot = false
    spotSavedCFrame = nil
    spotButton.Text             = "📍 Go to Spot"
    spotButton.BackgroundColor3 = Color3.fromRGB(20, 120, 60)
end)

-- === Coordinate Update Loop ===
RunService.RenderStepped:Connect(function()
    local character = player.Character
    if not character then
        coordsLabel.Text = "Waiting for character..."
        return
    end
    local root = character:FindFirstChild("HumanoidRootPart")
    if not root then return end
    local p = root.Position
    coordsLabel.Text = string.format("X: %.1f\nY: %.1f\nZ: %.1f", p.X, p.Y, p.Z)
end)

]==],
        color = Color3.fromRGB(30, 180, 120),
        icon  = "🛡️",
    },
}

local function buildScriptCard(data, idx)
    local Card = Instance.new("Frame", PageScript)
    Card.Size             = UDim2.new(1, -20, 0, 90)
    Card.BackgroundColor3 = Color3.fromRGB(28, 28, 42)
    Card.BorderSizePixel  = 0
    Card.LayoutOrder      = idx
    local CC = Instance.new("UICorner", Card); CC.CornerRadius = UDim.new(0, 10)
    local CS = Instance.new("UIStroke", Card); CS.Color = data.color; CS.Thickness = 1.5

    local Bar = Instance.new("Frame", Card)
    Bar.Size             = UDim2.new(0, 4, 0.7, 0)
    Bar.Position         = UDim2.new(0, 0, 0.15, 0)
    Bar.BackgroundColor3 = data.color
    Bar.BorderSizePixel  = 0
    local BC = Instance.new("UICorner", Bar); BC.CornerRadius = UDim.new(0, 4)

    local Icon = Instance.new("TextLabel", Card)
    Icon.Size             = UDim2.new(0, 36, 0, 36)
    Icon.Position         = UDim2.new(0, 14, 0, 10)
    Icon.BackgroundColor3 = data.color
    Icon.Text             = data.icon
    Icon.TextSize         = 18
    Icon.Font             = Enum.Font.GothamBold
    Icon.TextColor3       = Color3.fromRGB(255, 255, 255)
    Icon.BorderSizePixel  = 0
    local IC = Instance.new("UICorner", Icon); IC.CornerRadius = UDim.new(0, 8)

    local Name = Instance.new("TextLabel", Card)
    Name.Size             = UDim2.new(1, -70, 0, 20)
    Name.Position         = UDim2.new(0, 58, 0, 10)
    Name.BackgroundTransparency = 1
    Name.Text             = data.name
    Name.TextColor3       = Color3.fromRGB(230, 230, 255)
    Name.TextSize         = 13
    Name.Font             = Enum.Font.GothamBold
    Name.TextXAlignment   = Enum.TextXAlignment.Left

    local Desc = Instance.new("TextLabel", Card)
    Desc.Size             = UDim2.new(1, -70, 0, 14)
    Desc.Position         = UDim2.new(0, 58, 0, 30)
    Desc.BackgroundTransparency = 1
    Desc.Text             = data.desc
    Desc.TextColor3       = Color3.fromRGB(150, 150, 180)
    Desc.TextSize         = 10
    Desc.Font             = Enum.Font.Gotham
    Desc.TextXAlignment   = Enum.TextXAlignment.Left

    local StatusLbl = Instance.new("TextLabel", Card)
    StatusLbl.Size             = UDim2.new(1, -20, 0, 14)
    StatusLbl.Position         = UDim2.new(0, 10, 0, 50)
    StatusLbl.BackgroundTransparency = 1
    StatusLbl.Text             = ""
    StatusLbl.TextColor3       = Color3.fromRGB(150, 150, 180)
    StatusLbl.TextSize         = 9
    StatusLbl.Font             = Enum.Font.Gotham
    StatusLbl.TextXAlignment   = Enum.TextXAlignment.Left

    local RunBtn = Instance.new("TextButton", Card)
    RunBtn.Size             = UDim2.new(0, 90, 0, 28)
    RunBtn.Position         = UDim2.new(1, -98, 0, 10)
    RunBtn.BackgroundColor3 = data.color
    RunBtn.Text             = "▶  شغّل"
    RunBtn.TextColor3       = Color3.fromRGB(255, 255, 255)
    RunBtn.TextSize         = 12
    RunBtn.Font             = Enum.Font.GothamBold
    RunBtn.BorderSizePixel  = 0
    local RC = Instance.new("UICorner", RunBtn); RC.CornerRadius = UDim.new(0, 7)

    local scriptUrl = data.url or ""
    local scriptColor = data.color

    RunBtn.MouseButton1Click:Connect(function()
        RunBtn.Text             = "⏳ جارٍ..."
        RunBtn.BackgroundColor3 = Color3.fromRGB(60, 60, 80)
        StatusLbl.Text          = "⏳ يحمّل السكربت..."
        StatusLbl.TextColor3    = Color3.fromRGB(200, 200, 80)

        task.spawn(function()
            local ok, err = pcall(function()
                if scriptUrl ~= "" then
                    loadstring(game:HttpGet(scriptUrl))()
                else
                    loadstring(data.code)()
                end
            end)
            if ok then
                RunBtn.Text             = "✔  شغّال"
                RunBtn.BackgroundColor3 = Color3.fromRGB(50, 200, 90)
                StatusLbl.Text          = "✅ تم التشغيل بنجاح"
                StatusLbl.TextColor3    = Color3.fromRGB(50, 210, 100)
                task.delay(3, function()
                    if RunBtn and RunBtn.Parent then
                        RunBtn.Text             = "▶  شغّل"
                        RunBtn.BackgroundColor3 = scriptColor
                        StatusLbl.Text          = ""
                    end
                end)
            else
                RunBtn.Text             = "✖  فشل"
                RunBtn.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
                StatusLbl.Text          = "❌ " .. tostring(err):sub(1, 50)
                StatusLbl.TextColor3    = Color3.fromRGB(220, 70, 70)
                task.delay(4, function()
                    if RunBtn and RunBtn.Parent then
                        RunBtn.Text             = "▶  شغّل"
                        RunBtn.BackgroundColor3 = scriptColor
                        StatusLbl.Text          = ""
                    end
                end)
            end
        end)
    end)

    return Card
end

for i, s in ipairs(SCRIPTS) do
    buildScriptCard(s, i)
end

local SC = {
    PANEL  = Color3.fromRGB(22, 22, 32),
    CARD   = Color3.fromRGB(30, 30, 44),
    TEXT   = Color3.fromRGB(230, 230, 255),
    SUB    = Color3.fromRGB(150, 150, 180),
    ACCENT = Color3.fromRGB(100, 60, 220),
    GREEN  = Color3.fromRGB(50, 220, 100),
    RED    = Color3.fromRGB(220, 60, 60),
    YELLOW = Color3.fromRGB(255, 200, 50),
    BLUE   = Color3.fromRGB(50, 130, 255),
    ORANGE = Color3.fromRGB(255, 140, 0),
    DEVO   = Color3.fromRGB(148, 0, 211),
    COPY   = Color3.fromRGB(40, 180, 140),
    DIV    = Color3.fromRGB(40, 40, 60),
    STOP   = Color3.fromRGB(200, 40, 40),
    JOIN   = Color3.fromRGB(30, 200, 90),
    LEAVE  = Color3.fromRGB(220, 60, 60),
}

local function _tw(obj, props, t)
    TweenService:Create(obj, TweenInfo.new(t or 0.15), props):Play()
end
local function _corner(p, r)
    local c = Instance.new("UICorner", p)
    c.CornerRadius = UDim.new(0, r or 8)
end
local function _stroke(p, col, th)
    local s = Instance.new("UIStroke", p)
    s.Color = col or SC.ACCENT
    s.Thickness = th or 1
end
local function _getRoot2(p) local c = p and p.Character return c and c:FindFirstChild("HumanoidRootPart") end
local function _getHum2(p)  local c = p and p.Character return c and c:FindFirstChildOfClass("Humanoid") end

local NotifStack = Instance.new("Frame")
NotifStack.Parent = ScreenGui
NotifStack.Size   = UDim2.new(0, 310, 1, -20)
NotifStack.Position = UDim2.new(0.5, -165, 0, -48)
NotifStack.BackgroundTransparency = 1
NotifStack.BorderSizePixel = 0
local _NSLayout = Instance.new("UIListLayout", NotifStack)
_NSLayout.SortOrder = Enum.SortOrder.LayoutOrder
_NSLayout.VerticalAlignment = Enum.VerticalAlignment.Bottom
_NSLayout.FillDirection = Enum.FillDirection.Vertical
_NSLayout.Padding = UDim.new(0, 5)

local _nIdx = 0
local function spawnNotif(text, isJoin, userId)
    _nIdx = _nIdx + 1
    local col = isJoin and SC.JOIN or SC.LEAVE
    local Wrap = Instance.new("Frame", NotifStack)
    Wrap.Size = UDim2.new(1,0,0,58)
    Wrap.BackgroundTransparency = 1
    Wrap.BorderSizePixel = 0
    Wrap.LayoutOrder = _nIdx
    local Card = Instance.new("Frame", Wrap)
    Card.Size = UDim2.new(1,0,1,0)
    Card.BackgroundColor3 = SC.PANEL
    Card.BorderSizePixel = 0
    _corner(Card, 8) _stroke(Card, col, 1.2)
    local Bar = Instance.new("Frame", Card)
    Bar.Size = UDim2.new(0,4,0.7,0)
    Bar.Position = UDim2.new(0,6,0.15,0)
    Bar.BackgroundColor3 = col
    Bar.BorderSizePixel = 0
    _corner(Bar, 4)
    local txtOffsetX = 14
    local txtWidth   = -18
    if userId then
        local Img = Instance.new("ImageLabel", Card)
        Img.Size = UDim2.new(0,34,0,34)
        Img.Position = UDim2.new(0,14,0.5,-17)
        Img.BackgroundTransparency = 1
        Img.Image = "rbxthumb://type=AvatarHeadShot&id="..userId.."&w=48&h=48"
        _corner(Img, 17)
        txtOffsetX = 54
        txtWidth   = -60
    end
    local Txt = Instance.new("TextLabel", Card)
    Txt.Size = UDim2.new(1, txtWidth, 1, 0)
    Txt.Position = UDim2.new(0, txtOffsetX, 0, 0)
    Txt.BackgroundTransparency = 1
    Txt.Text = text
    Txt.TextColor3 = SC.TEXT
    Txt.TextSize = 11
    Txt.Font = Enum.Font.GothamBold
    Txt.TextXAlignment = Enum.TextXAlignment.Center
    Txt.TextYAlignment = Enum.TextYAlignment.Center
    Txt.TextWrapped = true
    task.delay(4.5, function()
        _tw(Card, {BackgroundTransparency=1}, 0.4)
        task.delay(0.5, function() Wrap:Destroy() end)
    end)
end

local DBar = Instance.new("Frame", PageScanner)
DBar.Size = UDim2.new(1,-20,0,44)
DBar.Position = UDim2.new(0,10,0,6)
DBar.BackgroundColor3 = SC.PANEL
DBar.BorderSizePixel = 0
_corner(DBar, 8)
_stroke(DBar, Color3.fromRGB(90,0,160), 1)

local DLbl = Instance.new("TextLabel", DBar)
DLbl.Size = UDim2.new(0.55,0,1,0)
DLbl.Position = UDim2.new(0,12,0,0)
DLbl.BackgroundTransparency = 1
DLbl.Text = "🔴  Devo Track:  OFF"
DLbl.TextColor3 = SC.SUB
DLbl.TextSize = 12
DLbl.Font = Enum.Font.GothamBold
DLbl.TextXAlignment = Enum.TextXAlignment.Left

local DBtn = Instance.new("TextButton", DBar)
DBtn.Size = UDim2.new(0,118,0,28)
DBtn.Position = UDim2.new(1,-126,0,8)
DBtn.BackgroundColor3 = SC.DEVO
DBtn.Text = "تفعيل التتبع"
DBtn.TextColor3 = SC.TEXT
DBtn.TextSize = 12
DBtn.Font = Enum.Font.GothamBold
DBtn.BorderSizePixel = 0
_corner(DBtn, 6)

local JBar = Instance.new("Frame", PageScanner)
JBar.Size = UDim2.new(1,-20,0,54)
JBar.Position = UDim2.new(0,10,0,56)
JBar.BackgroundColor3 = SC.PANEL
JBar.BorderSizePixel = 0
_corner(JBar, 8)
_stroke(JBar, SC.ORANGE, 1)

local JTitle = Instance.new("TextLabel", JBar)
JTitle.Size = UDim2.new(1,0,0,18)
JTitle.Position = UDim2.new(0,12,0,4)
JTitle.BackgroundTransparency = 1
JTitle.Text = "⚡  Devo Jitter  —  حركة قدام / ورا سريعة"
JTitle.TextColor3 = SC.ORANGE
JTitle.TextSize = 11
JTitle.Font = Enum.Font.GothamBold
JTitle.TextXAlignment = Enum.TextXAlignment.Left

local JLbl = Instance.new("TextLabel", JBar)
JLbl.Size = UDim2.new(0,90,0,18)
JLbl.Position = UDim2.new(0,12,0,28)
JLbl.BackgroundTransparency = 1
JLbl.Text = "🔴  Jitter: OFF"
JLbl.TextColor3 = SC.SUB
JLbl.TextSize = 11
JLbl.Font = Enum.Font.GothamBold
JLbl.TextXAlignment = Enum.TextXAlignment.Left

local jSpeedVal = 30
local JSpeedLbl = Instance.new("TextLabel", JBar)
JSpeedLbl.Size = UDim2.new(0,55,0,18)
JSpeedLbl.Position = UDim2.new(0,182,0,28)
JSpeedLbl.BackgroundTransparency = 1
JSpeedLbl.Text = "spd:"..jSpeedVal
JSpeedLbl.TextColor3 = SC.SUB
JSpeedLbl.TextSize = 10
JSpeedLbl.Font = Enum.Font.Gotham
JSpeedLbl.TextXAlignment = Enum.TextXAlignment.Left

local JSpeedDn = Instance.new("TextButton", JBar)
JSpeedDn.Size = UDim2.new(0,22,0,18)
JSpeedDn.Position = UDim2.new(0,158,0,28)
JSpeedDn.BackgroundColor3 = SC.DIV
JSpeedDn.Text = "−"
JSpeedDn.TextColor3 = SC.TEXT
JSpeedDn.TextSize = 14
JSpeedDn.Font = Enum.Font.GothamBold
JSpeedDn.BorderSizePixel = 0
_corner(JSpeedDn, 4)

local JSpeedUp = Instance.new("TextButton", JBar)
JSpeedUp.Size = UDim2.new(0,22,0,18)
JSpeedUp.Position = UDim2.new(0,240,0,28)
JSpeedUp.BackgroundColor3 = SC.DIV
JSpeedUp.Text = "+"
JSpeedUp.TextColor3 = SC.TEXT
JSpeedUp.TextSize = 14
JSpeedUp.Font = Enum.Font.GothamBold
JSpeedUp.BorderSizePixel = 0
_corner(JSpeedUp, 4)

local JBtn = Instance.new("TextButton", JBar)
JBtn.Size = UDim2.new(0,108,0,30)
JBtn.Position = UDim2.new(1,-116,0,12)
JBtn.BackgroundColor3 = SC.ORANGE
JBtn.Text = "تفعيل Jitter"
JBtn.TextColor3 = Color3.fromRGB(10,10,10)
JBtn.TextSize = 12
JBtn.Font = Enum.Font.GothamBold
JBtn.BorderSizePixel = 0
_corner(JBtn, 6)

local STopBar = Instance.new("Frame", PageScanner)
STopBar.Size = UDim2.new(1,-20,0,34)
STopBar.Position = UDim2.new(0,10,0,116)
STopBar.BackgroundColor3 = SC.PANEL
STopBar.BorderSizePixel = 0
_corner(STopBar, 8)

local CountLbl = Instance.new("TextLabel", STopBar)
CountLbl.Size = UDim2.new(0.6,0,1,0)
CountLbl.Position = UDim2.new(0,12,0,0)
CountLbl.BackgroundTransparency = 1
CountLbl.Text = "اللاعبون: 0"
CountLbl.TextColor3 = SC.TEXT
CountLbl.TextSize = 12
CountLbl.Font = Enum.Font.GothamBold
CountLbl.TextXAlignment = Enum.TextXAlignment.Left

local sortByDist  = false  
local SortToggle  = Instance.new("TextButton", STopBar)
SortToggle.Size              = UDim2.new(0,80,0,24)
SortToggle.Position          = UDim2.new(1,-196,0,5)
SortToggle.BackgroundColor3  = SC.DIV
SortToggle.Text              = "🔤 اسم"
SortToggle.TextColor3        = SC.TEXT
SortToggle.TextSize          = 11
SortToggle.Font              = Enum.Font.GothamBold
SortToggle.BorderSizePixel   = 0
_corner(SortToggle, 6)
SortToggle.MouseButton1Click:Connect(function()
    sortByDist = not sortByDist
    SortToggle.Text = sortByDist and "📏 مسافة" or "🔤 اسم"
    SortToggle.BackgroundColor3 = sortByDist and SC.ACCENT or SC.DIV
end)

local ScanBtn = Instance.new("TextButton", STopBar)
ScanBtn.Size = UDim2.new(0,100,0,24)
ScanBtn.Position = UDim2.new(1,-108,0,5)
ScanBtn.BackgroundColor3 = SC.GREEN
ScanBtn.Text = "🔍  سكان"
ScanBtn.TextColor3 = Color3.fromRGB(10,10,10)
ScanBtn.TextSize = 12
ScanBtn.Font = Enum.Font.GothamBold
ScanBtn.BorderSizePixel = 0
_corner(ScanBtn, 6)

local PlayerList = Instance.new("ScrollingFrame", PageScanner)
PlayerList.Size = UDim2.new(1,-20,1,-164)
PlayerList.Position = UDim2.new(0,10,0,158)
PlayerList.BackgroundColor3 = SC.PANEL
PlayerList.BorderSizePixel = 0
PlayerList.ScrollBarThickness = 4
PlayerList.ScrollBarImageColor3 = SC.ACCENT
PlayerList.CanvasSize = UDim2.new(0,0,0,0)
PlayerList.AutomaticCanvasSize = Enum.AutomaticSize.Y
_corner(PlayerList, 8)
local PLLayout = Instance.new("UIListLayout", PlayerList)
PLLayout.SortOrder = Enum.SortOrder.LayoutOrder
PLLayout.Padding = UDim.new(0,6)
local PLPad = Instance.new("UIPadding", PlayerList)
PLPad.PaddingTop    = UDim.new(0,8)
PLPad.PaddingBottom = UDim.new(0,8)
PLPad.PaddingLeft   = UDim.new(0,8)
PLPad.PaddingRight  = UDim.new(0,8)

local isTracking    = false
local isJitter      = false
local selectedDevo  = nil
local JITTER_AMP    = 3.5

JSpeedDn.MouseButton1Click:Connect(function()
    jSpeedVal = math.max(5, jSpeedVal - 5)
    JSpeedLbl.Text = "spd:"..jSpeedVal
end)
JSpeedUp.MouseButton1Click:Connect(function()
    jSpeedVal = math.min(80, jSpeedVal + 5)
    JSpeedLbl.Text = "spd:"..jSpeedVal
end)

RunService.Heartbeat:Connect(function()
    local myRoot = GetRoot()
    if not myRoot then return end
    if isTracking then
        local target
        if selectedDevo and _getRoot2(selectedDevo) then
            target = selectedDevo
        else
            local best = math.huge
            for _, p in ipairs(Players:GetPlayers()) do
                if p ~= LocalPlayer then
                    local r = _getRoot2(p)
                    if r then
                        local d = (r.Position - myRoot.Position).Magnitude
                        if d < best then best = d; target = p end
                    end
                end
            end
        end
        if target then
            local tr = _getRoot2(target)
            if tr then myRoot.CFrame = tr.CFrame * CFrame.new(0,0,2.5) end
        end
    end
    if isJitter then
        local offset = math.sin(os.clock() * jSpeedVal) * JITTER_AMP
        myRoot.CFrame = myRoot.CFrame * CFrame.new(0,0,offset)
    end
end)

DBtn.MouseButton1Click:Connect(function()
    isTracking = not isTracking
    if isTracking then
        DLbl.Text = "🟢  Devo Track:  ON"; DLbl.TextColor3 = SC.GREEN
        DBtn.Text = "إيقاف التتبع";        DBtn.BackgroundColor3 = SC.STOP
    else
        DLbl.Text = "🔴  Devo Track:  OFF"; DLbl.TextColor3 = SC.SUB
        DBtn.Text = "تفعيل التتبع";         DBtn.BackgroundColor3 = SC.DEVO
        selectedDevo = nil
    end
end)

JBtn.MouseButton1Click:Connect(function()
    isJitter = not isJitter
    if isJitter then
        JLbl.Text = "🟠  Jitter: ON"; JLbl.TextColor3 = SC.ORANGE
        JBtn.Text = "إيقاف Jitter";  JBtn.BackgroundColor3 = SC.STOP
        _tw(JBar, {BackgroundColor3 = Color3.fromRGB(35,25,10)})
    else
        JLbl.Text = "🔴  Jitter: OFF"; JLbl.TextColor3 = SC.SUB
        JBtn.Text = "تفعيل Jitter";    JBtn.BackgroundColor3 = SC.ORANGE
        _tw(JBar, {BackgroundColor3 = SC.PANEL})
    end
end)

local function hpColor(pct)
    if pct > 0.6 then return SC.GREEN
    elseif pct > 0.3 then return SC.YELLOW
    else return SC.RED end
end

local _trollOpenSet  = {}  
local _pinnedPlayer  = nil  

local function buildCard(p, idx)
    local hum    = _getHum2(p)
    local root   = _getRoot2(p)
    local myRoot = GetRoot()
    local dist   = (root and myRoot) and math.floor((root.Position - myRoot.Position).Magnitude) or "?"
    local alive  = hum and hum.Health > 0

    local Card = Instance.new("Frame", PlayerList)
    Card.Size = UDim2.new(1,0,0,100)  
    Card.BackgroundColor3 = SC.CARD
    Card.BorderSizePixel = 0
    Card.LayoutOrder = idx
    Card:SetAttribute("PlayerName", p.Name)
    _corner(Card, 8) _stroke(Card, SC.DIV, 1)

    local NumLbl = Instance.new("TextLabel", Card)
    NumLbl.Size = UDim2.new(0,26,0,26)
    NumLbl.Position = UDim2.new(0,8,0,8)
    NumLbl.BackgroundColor3 = SC.ACCENT
    NumLbl.Text = tostring(idx)
    NumLbl.TextColor3 = SC.TEXT
    NumLbl.TextSize = 11
    NumLbl.Font = Enum.Font.GothamBold
    NumLbl.BorderSizePixel = 0
    _corner(NumLbl, 6)

    local UserName = Instance.new("TextLabel", Card)
    UserName.Size = UDim2.new(1,-120,0,20)
    UserName.Position = UDim2.new(0,42,0,7)
    UserName.BackgroundTransparency = 1
    UserName.Text = p.Name
    UserName.TextColor3 = SC.TEXT
    UserName.TextSize = 14
    UserName.Font = Enum.Font.GothamBold
    UserName.TextXAlignment = Enum.TextXAlignment.Left
    UserName.TextTruncate = Enum.TextTruncate.AtEnd

    local DispName = Instance.new("TextLabel", Card)
    DispName.Size = UDim2.new(1,-120,0,16)
    DispName.Position = UDim2.new(0,42,0,26)
    DispName.BackgroundTransparency = 1
    DispName.Text = p.DisplayName
    DispName.TextColor3 = Color3.fromRGB(200, 200, 220)
    DispName.TextSize = 13
    DispName.Font = Enum.Font.GothamSemibold
    DispName.TextXAlignment = Enum.TextXAlignment.Left
    DispName.TextTruncate = Enum.TextTruncate.AtEnd

    local AliveLbl = Instance.new("TextLabel", Card)
    AliveLbl.Size = UDim2.new(0,70,0,16)
    AliveLbl.Position = UDim2.new(1,-76,0,6)
    AliveLbl.BackgroundTransparency = 1
    AliveLbl.Text = alive and "✔ حي" or "✘ ميت"
    AliveLbl.TextColor3 = alive and SC.GREEN or SC.RED
    AliveLbl.TextSize = 11
    AliveLbl.Font = Enum.Font.GothamBold
    AliveLbl.TextXAlignment = Enum.TextXAlignment.Right

    local InfoLbl = Instance.new("TextLabel", Card)
    InfoLbl.Size = UDim2.new(1,-16,0,18)
    InfoLbl.Position = UDim2.new(0,8,0,44)
    InfoLbl.BackgroundTransparency = 1
    InfoLbl.Text = string.format("📏 مسافة: %s  |  🆔 %d", tostring(dist), p.UserId)
    InfoLbl.TextColor3 = SC.SUB
    InfoLbl.TextSize = 10
    InfoLbl.Font = Enum.Font.Gotham
    InfoLbl.TextXAlignment = Enum.TextXAlignment.Left

    local btnY = 64

    local TPBtn = Instance.new("TextButton", Card)
    TPBtn.Size = UDim2.new(0,110,0,28)
    TPBtn.Position = UDim2.new(0,8,0,btnY)
    TPBtn.BackgroundColor3 = SC.BLUE
    TPBtn.Text = "⟶ TP إليه"
    TPBtn.TextColor3 = SC.TEXT
    TPBtn.TextSize = 11
    TPBtn.Font = Enum.Font.GothamBold
    TPBtn.BorderSizePixel = 0
    _corner(TPBtn, 6)
    TPBtn.MouseButton1Click:Connect(function()
        local mr = GetRoot(); local tr = _getRoot2(p)
        if mr and tr then mr.CFrame = tr.CFrame * CFrame.new(0,0,2.5) end
    end)
    TPBtn.MouseEnter:Connect(function()  _tw(TPBtn, {BackgroundColor3=Color3.fromRGB(80,160,255)}) end)
    TPBtn.MouseLeave:Connect(function() _tw(TPBtn, {BackgroundColor3=SC.BLUE}) end)

    local DSetBtn = Instance.new("TextButton", Card)
    DSetBtn.Size = UDim2.new(0,115,0,28)
    DSetBtn.Position = UDim2.new(0,128,0,btnY)
    DSetBtn.BackgroundColor3 = SC.DEVO
    DSetBtn.Text = "⬡ Devo هذا"
    DSetBtn.TextColor3 = SC.TEXT
    DSetBtn.TextSize = 11
    DSetBtn.Font = Enum.Font.GothamBold
    DSetBtn.BorderSizePixel = 0
    _corner(DSetBtn, 6)
    DSetBtn.MouseButton1Click:Connect(function()
        selectedDevo = p; isTracking = true
        DLbl.Text = "🟢  Devo: @"..p.Name; DLbl.TextColor3 = SC.GREEN
        DBtn.Text = "إيقاف التتبع";         DBtn.BackgroundColor3 = SC.STOP
    end)
    DSetBtn.MouseEnter:Connect(function()  _tw(DSetBtn, {BackgroundColor3=Color3.fromRGB(180,0,255)}) end)
    DSetBtn.MouseLeave:Connect(function() _tw(DSetBtn, {BackgroundColor3=SC.DEVO}) end)

    local CopyBtn = Instance.new("TextButton", Card)
    CopyBtn.Size = UDim2.new(0,110,0,28)
    CopyBtn.Position = UDim2.new(0,310,0,btnY)
    CopyBtn.BackgroundColor3 = SC.COPY
    CopyBtn.Text = "📋 نسخ ID"
    CopyBtn.TextColor3 = Color3.fromRGB(10,10,10)
    CopyBtn.TextSize = 11
    CopyBtn.Font = Enum.Font.GothamBold
    CopyBtn.BorderSizePixel = 0
    _corner(CopyBtn, 6)
    CopyBtn.MouseButton1Click:Connect(function()
        if setclipboard then setclipboard(tostring(p.UserId))
        elseif syn and syn.clipboard then syn.clipboard.set(tostring(p.UserId)) end
        CopyBtn.Text = "✔ نُسخ!"; _tw(CopyBtn, {BackgroundColor3=SC.GREEN})
        task.delay(1.5, function()
            if CopyBtn and CopyBtn.Parent then
                CopyBtn.Text = "📋 نسخ ID"; _tw(CopyBtn, {BackgroundColor3=SC.COPY})
            end
        end)
    end)
    CopyBtn.MouseEnter:Connect(function()  _tw(CopyBtn, {BackgroundColor3=Color3.fromRGB(60,220,170)}) end)
    CopyBtn.MouseLeave:Connect(function() _tw(CopyBtn, {BackgroundColor3=SC.COPY}) end)

    local TrollBtn = Instance.new("TextButton", Card)
    TrollBtn.Size = UDim2.new(0,100,0,28)
    TrollBtn.Position = UDim2.new(0,430,0,btnY)
    TrollBtn.BackgroundColor3 = Color3.fromRGB(80, 30, 120)
    TrollBtn.Text = "🎭 ترول ▼"
    TrollBtn.TextColor3 = SC.TEXT
    TrollBtn.TextSize = 11
    TrollBtn.Font = Enum.Font.GothamBold
    TrollBtn.BorderSizePixel = 0
    _corner(TrollBtn, 6)

    local TitleBtn = Instance.new("TextButton", Card)
    TitleBtn.Size = UDim2.new(0.5,-12,0,28)
    TitleBtn.Position = UDim2.new(0,8,0,96)
    TitleBtn.BackgroundColor3 = Color3.fromRGB(180, 120, 0)
    TitleBtn.Text = "✏️  تغيير العنوان (Title)"
    TitleBtn.TextColor3 = SC.TEXT
    TitleBtn.TextSize = 11
    TitleBtn.Font = Enum.Font.GothamBold
    TitleBtn.BorderSizePixel = 0
    _corner(TitleBtn, 6)

    TitleBtn.MouseButton1Click:Connect(function()
        
        local Overlay = Instance.new("Frame", ScreenGui)
        Overlay.Size = UDim2.new(1, 0, 1, 0)
        Overlay.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
        Overlay.BackgroundTransparency = 0.5
        Overlay.ZIndex = 999
        Overlay.BorderSizePixel = 0

        local PopupFrame = Instance.new("Frame", Overlay)
        PopupFrame.Size = UDim2.new(0, 360, 0, 140)
        PopupFrame.Position = UDim2.new(0.5, -180, 0.5, -70)
        PopupFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
        PopupFrame.BorderSizePixel = 0
        PopupFrame.ZIndex = 1000
        _corner(PopupFrame, 10)
        _stroke(PopupFrame, SC.ACCENT, 2)

        local PopTitle = Instance.new("TextLabel", PopupFrame)
        PopTitle.Size = UDim2.new(1, -16, 0, 30)
        PopTitle.Position = UDim2.new(0, 8, 0, 8)
        PopTitle.BackgroundTransparency = 1
        PopTitle.Text = "✏️  عنوان جديد لـ @" .. p.Name
        PopTitle.TextColor3 = SC.TEXT
        PopTitle.TextSize = 13
        PopTitle.Font = Enum.Font.GothamBold
        PopTitle.TextXAlignment = Enum.TextXAlignment.Left
        PopTitle.ZIndex = 1001

        local PopInput = Instance.new("TextBox", PopupFrame)
        PopInput.Size = UDim2.new(1, -16, 0, 36)
        PopInput.Position = UDim2.new(0, 8, 0, 44)
        PopInput.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
        PopInput.TextColor3 = SC.TEXT
        PopInput.Text = ""
        PopInput.PlaceholderText = "اكتب العنوان هنا..."
        PopInput.TextSize = 13
        PopInput.Font = Enum.Font.Gotham
        PopInput.BorderSizePixel = 0
        PopInput.ClearTextOnFocus = false
        PopInput.ZIndex = 1001
        _corner(PopInput, 6)
        _stroke(PopInput, SC.DIV, 1)

        local ConfirmBtn = Instance.new("TextButton", PopupFrame)
        ConfirmBtn.Size = UDim2.new(0, 160, 0, 30)
        ConfirmBtn.Position = UDim2.new(0, 8, 0, 96)
        ConfirmBtn.BackgroundColor3 = Color3.fromRGB(180, 120, 0)
        ConfirmBtn.Text = "✔ تطبيق"

        ConfirmBtn.TextColor3 = SC.TEXT
        ConfirmBtn.TextSize = 12
        ConfirmBtn.Font = Enum.Font.GothamBold
        ConfirmBtn.BorderSizePixel = 0
        ConfirmBtn.ZIndex = 1001
        _corner(ConfirmBtn, 6)

        local CancelBtn = Instance.new("TextButton", PopupFrame)
        CancelBtn.Size = UDim2.new(0, 160, 0, 30)
        CancelBtn.Position = UDim2.new(0, 184, 0, 96)
        CancelBtn.BackgroundColor3 = SC.RED
        CancelBtn.Text = "✖ إلغاء"
        CancelBtn.TextColor3 = SC.TEXT
        CancelBtn.TextSize = 12
        CancelBtn.Font = Enum.Font.GothamBold
        CancelBtn.BorderSizePixel = 0
        CancelBtn.ZIndex = 1001
        _corner(CancelBtn, 6)

        local function closePopup()
            Overlay:Destroy()
        end

        CancelBtn.MouseButton1Click:Connect(closePopup)

        ConfirmBtn.MouseButton1Click:Connect(function()
            local txt = PopInput.Text
            if txt and txt ~= "" then
                local full = "title " .. p.Name .. " " .. txt

                closePopup()
                task.wait(0.15)

                local vim = game:GetService("VirtualInputManager")
                local UIS = game:GetService("UserInputService")

                vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
                task.wait(0.2)

                local cmdBox = UIS:GetFocusedTextBox()
                if cmdBox then
                    
                    cmdBox.Text = cmdBox.Text .. full
                    
                    cmdBox.CursorPosition = #cmdBox.Text + 1
                end
                task.wait(0.05)

                vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

                TitleBtn.Text = "✔ تم: " .. txt
                _tw(TitleBtn, {BackgroundColor3 = SC.GREEN})
                task.delay(2, function()
                    if TitleBtn and TitleBtn.Parent then
                        TitleBtn.Text = "✏️  تغيير العنوان (Title)"
                        _tw(TitleBtn, {BackgroundColor3 = Color3.fromRGB(180, 120, 0)})
                    end
                end)
            else
                closePopup()
            end
        end)

        PopInput.FocusLost:Connect(function(enter)
            if enter then ConfirmBtn.MouseButton1Click:Fire() end
        end)

        PopInput:CaptureFocus()
    end)

    TitleBtn.MouseEnter:Connect(function()  _tw(TitleBtn, {BackgroundColor3=Color3.fromRGB(220,150,0)}) end)
    TitleBtn.MouseLeave:Connect(function() _tw(TitleBtn, {BackgroundColor3=Color3.fromRGB(180,120,0)}) end)

    local NameBtn = Instance.new("TextButton", Card)
    NameBtn.Size = UDim2.new(0.5,-12,0,28)
    NameBtn.Position = UDim2.new(0.5,4,0,96)
    NameBtn.BackgroundColor3 = Color3.fromRGB(0, 100, 160)
    NameBtn.Text = "✏️  تغيير الاسم (Name)"
    NameBtn.TextColor3 = SC.TEXT
    NameBtn.TextSize = 11
    NameBtn.Font = Enum.Font.GothamBold
    NameBtn.BorderSizePixel = 0
    _corner(NameBtn, 6)

    NameBtn.MouseButton1Click:Connect(function()
        local Overlay = Instance.new("Frame", ScreenGui)
        Overlay.Size = UDim2.new(1, 0, 1, 0)
        Overlay.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
        Overlay.BackgroundTransparency = 0.5
        Overlay.ZIndex = 999
        Overlay.BorderSizePixel = 0

        local PopupFrame = Instance.new("Frame", Overlay)
        PopupFrame.Size = UDim2.new(0, 360, 0, 140)
        PopupFrame.Position = UDim2.new(0.5, -180, 0.5, -70)
        PopupFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 30)
        PopupFrame.BorderSizePixel = 0
        PopupFrame.ZIndex = 1000
        _corner(PopupFrame, 10)
        _stroke(PopupFrame, SC.ACCENT, 2)

        local PopTitle = Instance.new("TextLabel", PopupFrame)
        PopTitle.Size = UDim2.new(1, -16, 0, 30)
        PopTitle.Position = UDim2.new(0, 8, 0, 8)
        PopTitle.BackgroundTransparency = 1
        PopTitle.Text = "✏️  اسم جديد لـ @" .. p.Name
        PopTitle.TextColor3 = SC.TEXT
        PopTitle.TextSize = 13
        PopTitle.Font = Enum.Font.GothamBold
        PopTitle.TextXAlignment = Enum.TextXAlignment.Left
        PopTitle.ZIndex = 1001

        local PopInput = Instance.new("TextBox", PopupFrame)
        PopInput.Size = UDim2.new(1, -16, 0, 36)
        PopInput.Position = UDim2.new(0, 8, 0, 44)
        PopInput.BackgroundColor3 = Color3.fromRGB(35, 35, 50)
        PopInput.TextColor3 = SC.TEXT
        PopInput.Text = ""
        PopInput.PlaceholderText = "اكتب الاسم هنا..."
        PopInput.TextSize = 13
        PopInput.Font = Enum.Font.Gotham
        PopInput.BorderSizePixel = 0
        PopInput.ClearTextOnFocus = false
        PopInput.ZIndex = 1001
        _corner(PopInput, 6)
        _stroke(PopInput, SC.DIV, 1)

        local ConfirmBtn = Instance.new("TextButton", PopupFrame)
        ConfirmBtn.Size = UDim2.new(0, 160, 0, 30)
        ConfirmBtn.Position = UDim2.new(0, 8, 0, 96)
        ConfirmBtn.BackgroundColor3 = Color3.fromRGB(0, 100, 160)
        ConfirmBtn.Text = "✔ تطبيق"
        ConfirmBtn.TextColor3 = SC.TEXT
        ConfirmBtn.TextSize = 12
        ConfirmBtn.Font = Enum.Font.GothamBold
        ConfirmBtn.BorderSizePixel = 0
        ConfirmBtn.ZIndex = 1001
        _corner(ConfirmBtn, 6)

        local CancelBtn = Instance.new("TextButton", PopupFrame)
        CancelBtn.Size = UDim2.new(0, 160, 0, 30)
        CancelBtn.Position = UDim2.new(0, 184, 0, 96)
        CancelBtn.BackgroundColor3 = SC.RED
        CancelBtn.Text = "✖ إلغاء"
        CancelBtn.TextColor3 = SC.TEXT
        CancelBtn.TextSize = 12
        CancelBtn.Font = Enum.Font.GothamBold
        CancelBtn.BorderSizePixel = 0
        CancelBtn.ZIndex = 1001
        _corner(CancelBtn, 6)

        local function closePopup()
            Overlay:Destroy()
        end

        CancelBtn.MouseButton1Click:Connect(closePopup)

        ConfirmBtn.MouseButton1Click:Connect(function()
            local txt = PopInput.Text
            if txt and txt ~= "" then
                local full = "name " .. p.Name .. " " .. txt

                closePopup()
                task.wait(0.15)

                local vim = game:GetService("VirtualInputManager")
                local UIS = game:GetService("UserInputService")

                vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
                task.wait(0.2)

                local cmdBox = UIS:GetFocusedTextBox()
                if cmdBox then
                    cmdBox.Text = cmdBox.Text .. full
                    cmdBox.CursorPosition = #cmdBox.Text + 1
                end
                task.wait(0.05)

                vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
                vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

                NameBtn.Text = "✔ تم: " .. txt
                _tw(NameBtn, {BackgroundColor3 = SC.GREEN})
                task.delay(2, function()
                    if NameBtn and NameBtn.Parent then
                        NameBtn.Text = "✏️  تغيير الاسم (Name)"
                        _tw(NameBtn, {BackgroundColor3 = Color3.fromRGB(0, 100, 160)})
                    end
                end)
            else
                closePopup()
            end
        end)

        PopInput.FocusLost:Connect(function(enter)
            if enter then ConfirmBtn.MouseButton1Click:Fire() end
        end)

        PopInput:CaptureFocus()
    end)

    NameBtn.MouseEnter:Connect(function()  _tw(NameBtn, {BackgroundColor3=Color3.fromRGB(0,140,210)}) end)
    NameBtn.MouseLeave:Connect(function() _tw(NameBtn, {BackgroundColor3=Color3.fromRGB(0,100,160)}) end)

    local DogBtn = Instance.new("TextButton", Card)
    DogBtn.Size = UDim2.new(0.5,-12,0,28)
    DogBtn.Position = UDim2.new(0,8,0,128)
    DogBtn.BackgroundColor3 = Color3.fromRGB(80, 50, 20)
    DogBtn.Text = "🐕  Dog"
    DogBtn.TextColor3 = SC.TEXT
    DogBtn.TextSize = 11
    DogBtn.Font = Enum.Font.GothamBold
    DogBtn.BorderSizePixel = 0
    _corner(DogBtn, 6)

    DogBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "dog " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        DogBtn.Text = "✔ تم!"
        _tw(DogBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if DogBtn and DogBtn.Parent then
                DogBtn.Text = "🐕  Dog"
                _tw(DogBtn, {BackgroundColor3 = Color3.fromRGB(80,50,20)})
            end
        end)
    end)

    DogBtn.MouseEnter:Connect(function()  _tw(DogBtn, {BackgroundColor3=Color3.fromRGB(120,80,30)}) end)
    DogBtn.MouseLeave:Connect(function() _tw(DogBtn, {BackgroundColor3=Color3.fromRGB(80,50,20)}) end)

    local ViewBtn = Instance.new("TextButton", Card)
    ViewBtn.Size = UDim2.new(0.5,-12,0,28)
    ViewBtn.Position = UDim2.new(0,8,0,160)
    ViewBtn.BackgroundColor3 = Color3.fromRGB(20, 80, 130)
    ViewBtn.Text = "👁️  View"
    ViewBtn.TextColor3 = SC.TEXT
    ViewBtn.TextSize = 11
    ViewBtn.Font = Enum.Font.GothamBold
    ViewBtn.BorderSizePixel = 0
    _corner(ViewBtn, 6)

    ViewBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "view " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        ViewBtn.Text = "✔ تم!"
        _tw(ViewBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if ViewBtn and ViewBtn.Parent then
                ViewBtn.Text = "👁️  View"
                _tw(ViewBtn, {BackgroundColor3 = Color3.fromRGB(20,80,130)})
            end
        end)
    end)

    ViewBtn.MouseEnter:Connect(function()  _tw(ViewBtn, {BackgroundColor3=Color3.fromRGB(30,120,180)}) end)
    ViewBtn.MouseLeave:Connect(function() _tw(ViewBtn, {BackgroundColor3=Color3.fromRGB(20,80,130)}) end)

    local UnviewBtn = Instance.new("TextButton", Card)
    UnviewBtn.Size = UDim2.new(0.5,-12,0,28)
    UnviewBtn.Position = UDim2.new(0.5,4,0,160)
    UnviewBtn.BackgroundColor3 = Color3.fromRGB(20, 60, 100)
    UnviewBtn.Text = "🚫  Unview"
    UnviewBtn.TextColor3 = SC.TEXT
    UnviewBtn.TextSize = 11
    UnviewBtn.Font = Enum.Font.GothamBold
    UnviewBtn.BorderSizePixel = 0
    _corner(UnviewBtn, 6)

    UnviewBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "unview " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        UnviewBtn.Text = "✔ تم!"
        _tw(UnviewBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if UnviewBtn and UnviewBtn.Parent then
                UnviewBtn.Text = "🚫  Unview"
                _tw(UnviewBtn, {BackgroundColor3 = Color3.fromRGB(20,60,100)})
            end
        end)
    end)

    UnviewBtn.MouseEnter:Connect(function()  _tw(UnviewBtn, {BackgroundColor3=Color3.fromRGB(30,90,150)}) end)
    UnviewBtn.MouseLeave:Connect(function() _tw(UnviewBtn, {BackgroundColor3=Color3.fromRGB(20,60,100)}) end)

    local RespawnBtn = Instance.new("TextButton", Card)
    RespawnBtn.Size = UDim2.new(0.5,-12,0,28)
    RespawnBtn.Position = UDim2.new(0.5,4,0,128)
    RespawnBtn.BackgroundColor3 = Color3.fromRGB(20, 100, 60)
    RespawnBtn.Text = "🔄  Respawn"
    RespawnBtn.TextColor3 = SC.TEXT
    RespawnBtn.TextSize = 11
    RespawnBtn.Font = Enum.Font.GothamBold
    RespawnBtn.BorderSizePixel = 0
    _corner(RespawnBtn, 6)

    RespawnBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "respawn " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        RespawnBtn.Text = "✔ تم!"
        _tw(RespawnBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if RespawnBtn and RespawnBtn.Parent then
                RespawnBtn.Text = "🔄  Respawn"
                _tw(RespawnBtn, {BackgroundColor3 = Color3.fromRGB(20,100,60)})
            end
        end)
    end)

    RespawnBtn.MouseEnter:Connect(function()  _tw(RespawnBtn, {BackgroundColor3=Color3.fromRGB(30,140,80)}) end)
    RespawnBtn.MouseLeave:Connect(function() _tw(RespawnBtn, {BackgroundColor3=Color3.fromRGB(20,100,60)}) end)

    local TakeLBtn = Instance.new("TextButton", Card)
    TakeLBtn.Size = UDim2.new(0.5,-12,0,28)
    TakeLBtn.Position = UDim2.new(0,8,0,192)
    TakeLBtn.BackgroundColor3 = Color3.fromRGB(140, 20, 20)
    TakeLBtn.Text = "😢  TakeTheL"
    TakeLBtn.TextColor3 = SC.TEXT
    TakeLBtn.TextSize = 11
    TakeLBtn.Font = Enum.Font.GothamBold
    TakeLBtn.BorderSizePixel = 0
    _corner(TakeLBtn, 6)

    TakeLBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "TakeTheL " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        TakeLBtn.Text = "✔ تم!"
        _tw(TakeLBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if TakeLBtn and TakeLBtn.Parent then
                TakeLBtn.Text = "😢  TakeTheL"
                _tw(TakeLBtn, {BackgroundColor3 = Color3.fromRGB(140,20,20)})
            end
        end)
    end)

    TakeLBtn.MouseEnter:Connect(function()  _tw(TakeLBtn, {BackgroundColor3=Color3.fromRGB(190,30,30)}) end)
    TakeLBtn.MouseLeave:Connect(function() _tw(TakeLBtn, {BackgroundColor3=Color3.fromRGB(140,20,20)}) end)

    local ChibifyBtn = Instance.new("TextButton", Card)
    ChibifyBtn.Size = UDim2.new(0.5,-12,0,28)
    ChibifyBtn.Position = UDim2.new(0.5,4,0,192)
    ChibifyBtn.BackgroundColor3 = Color3.fromRGB(120,60,160)
    ChibifyBtn.Text = "🧸  Chibify"
    ChibifyBtn.TextColor3 = SC.TEXT
    ChibifyBtn.TextSize = 11
    ChibifyBtn.Font = Enum.Font.GothamBold
    ChibifyBtn.BorderSizePixel = 0
    _corner(ChibifyBtn, 6)

    ChibifyBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "chibify " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        ChibifyBtn.Text = "✔ تم!"
        _tw(ChibifyBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if ChibifyBtn and ChibifyBtn.Parent then
                ChibifyBtn.Text = "🧸  Chibify"
                _tw(ChibifyBtn, {BackgroundColor3 = Color3.fromRGB(120,60,160)})
            end
        end)
    end)

    ChibifyBtn.MouseEnter:Connect(function()  _tw(ChibifyBtn, {BackgroundColor3=Color3.fromRGB(math.min(120+40,255),math.min(60+40,255),math.min(160+40,255))}) end)
    ChibifyBtn.MouseLeave:Connect(function() _tw(ChibifyBtn, {BackgroundColor3=Color3.fromRGB(120,60,160)}) end)
    
    local FreakifyBtn = Instance.new("TextButton", Card)
    FreakifyBtn.Size = UDim2.new(0.5,-12,0,28)
    FreakifyBtn.Position = UDim2.new(0,8,0,224)
    FreakifyBtn.BackgroundColor3 = Color3.fromRGB(180,80,0)
    FreakifyBtn.Text = "👹  Freakify"
    FreakifyBtn.TextColor3 = SC.TEXT
    FreakifyBtn.TextSize = 11
    FreakifyBtn.Font = Enum.Font.GothamBold
    FreakifyBtn.BorderSizePixel = 0
    _corner(FreakifyBtn, 6)

    FreakifyBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "freakify " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        FreakifyBtn.Text = "✔ تم!"
        _tw(FreakifyBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if FreakifyBtn and FreakifyBtn.Parent then
                FreakifyBtn.Text = "👹  Freakify"
                _tw(FreakifyBtn, {BackgroundColor3 = Color3.fromRGB(180,80,0)})
            end
        end)
    end)

    FreakifyBtn.MouseEnter:Connect(function()  _tw(FreakifyBtn, {BackgroundColor3=Color3.fromRGB(math.min(180+40,255),math.min(80+40,255),math.min(0+40,255))}) end)
    FreakifyBtn.MouseLeave:Connect(function() _tw(FreakifyBtn, {BackgroundColor3=Color3.fromRGB(180,80,0)}) end)
    
    local BigifyBtn = Instance.new("TextButton", Card)
    BigifyBtn.Size = UDim2.new(0.5,-12,0,28)
    BigifyBtn.Position = UDim2.new(0.5,4,0,224)
    BigifyBtn.BackgroundColor3 = Color3.fromRGB(30,80,160)
    BigifyBtn.Text = "📏  Bigify"
    BigifyBtn.TextColor3 = SC.TEXT
    BigifyBtn.TextSize = 11
    BigifyBtn.Font = Enum.Font.GothamBold
    BigifyBtn.BorderSizePixel = 0
    _corner(BigifyBtn, 6)

    BigifyBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "bigify " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        BigifyBtn.Text = "✔ تم!"
        _tw(BigifyBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if BigifyBtn and BigifyBtn.Parent then
                BigifyBtn.Text = "📏  Bigify"
                _tw(BigifyBtn, {BackgroundColor3 = Color3.fromRGB(30,80,160)})
            end
        end)
    end)

    BigifyBtn.MouseEnter:Connect(function()  _tw(BigifyBtn, {BackgroundColor3=Color3.fromRGB(math.min(30+40,255),math.min(80+40,255),math.min(160+40,255))}) end)
    BigifyBtn.MouseLeave:Connect(function() _tw(BigifyBtn, {BackgroundColor3=Color3.fromRGB(30,80,160)}) end)
    
    local FatifyBtn = Instance.new("TextButton", Card)
    FatifyBtn.Size = UDim2.new(0.5,-12,0,28)
    FatifyBtn.Position = UDim2.new(0,8,0,256)
    FatifyBtn.BackgroundColor3 = Color3.fromRGB(160,60,30)
    FatifyBtn.Text = "🍔  Fatify"
    FatifyBtn.TextColor3 = SC.TEXT
    FatifyBtn.TextSize = 11
    FatifyBtn.Font = Enum.Font.GothamBold
    FatifyBtn.BorderSizePixel = 0
    _corner(FatifyBtn, 6)

    FatifyBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "fatify " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        FatifyBtn.Text = "✔ تم!"
        _tw(FatifyBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if FatifyBtn and FatifyBtn.Parent then
                FatifyBtn.Text = "🍔  Fatify"
                _tw(FatifyBtn, {BackgroundColor3 = Color3.fromRGB(160,60,30)})
            end
        end)
    end)

    FatifyBtn.MouseEnter:Connect(function()  _tw(FatifyBtn, {BackgroundColor3=Color3.fromRGB(math.min(160+40,255),math.min(60+40,255),math.min(30+40,255))}) end)
    FatifyBtn.MouseLeave:Connect(function() _tw(FatifyBtn, {BackgroundColor3=Color3.fromRGB(160,60,30)}) end)
    
    local NeonBtn = Instance.new("TextButton", Card)
    NeonBtn.Size = UDim2.new(0.5,-12,0,28)
    NeonBtn.Position = UDim2.new(0.5,4,0,256)
    NeonBtn.BackgroundColor3 = Color3.fromRGB(0,160,160)
    NeonBtn.Text = "💡  Neon"
    NeonBtn.TextColor3 = SC.TEXT
    NeonBtn.TextSize = 11
    NeonBtn.Font = Enum.Font.GothamBold
    NeonBtn.BorderSizePixel = 0
    _corner(NeonBtn, 6)

    NeonBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "neon " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        NeonBtn.Text = "✔ تم!"
        _tw(NeonBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if NeonBtn and NeonBtn.Parent then
                NeonBtn.Text = "💡  Neon"
                _tw(NeonBtn, {BackgroundColor3 = Color3.fromRGB(0,160,160)})
            end
        end)
    end)

    NeonBtn.MouseEnter:Connect(function()  _tw(NeonBtn, {BackgroundColor3=Color3.fromRGB(math.min(0+40,255),math.min(160+40,255),math.min(160+40,255))}) end)
    NeonBtn.MouseLeave:Connect(function() _tw(NeonBtn, {BackgroundColor3=Color3.fromRGB(0,160,160)}) end)
    
    local GoldBtn = Instance.new("TextButton", Card)
    GoldBtn.Size = UDim2.new(0.5,-12,0,28)
    GoldBtn.Position = UDim2.new(0,8,0,288)
    GoldBtn.BackgroundColor3 = Color3.fromRGB(160,130,0)
    GoldBtn.Text = "🥇  Gold"
    GoldBtn.TextColor3 = SC.TEXT
    GoldBtn.TextSize = 11
    GoldBtn.Font = Enum.Font.GothamBold
    GoldBtn.BorderSizePixel = 0
    _corner(GoldBtn, 6)

    GoldBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "gold " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        GoldBtn.Text = "✔ تم!"
        _tw(GoldBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if GoldBtn and GoldBtn.Parent then
                GoldBtn.Text = "🥇  Gold"
                _tw(GoldBtn, {BackgroundColor3 = Color3.fromRGB(160,130,0)})
            end
        end)
    end)

    GoldBtn.MouseEnter:Connect(function()  _tw(GoldBtn, {BackgroundColor3=Color3.fromRGB(math.min(160+40,255),math.min(130+40,255),math.min(0+40,255))}) end)
    GoldBtn.MouseLeave:Connect(function() _tw(GoldBtn, {BackgroundColor3=Color3.fromRGB(160,130,0)}) end)
    
    local BigheadBtn = Instance.new("TextButton", Card)
    BigheadBtn.Size = UDim2.new(0.5,-12,0,28)
    BigheadBtn.Position = UDim2.new(0.5,4,0,288)
    BigheadBtn.BackgroundColor3 = Color3.fromRGB(100,30,100)
    BigheadBtn.Text = "🗿  Bighead"
    BigheadBtn.TextColor3 = SC.TEXT
    BigheadBtn.TextSize = 11
    BigheadBtn.Font = Enum.Font.GothamBold
    BigheadBtn.BorderSizePixel = 0
    _corner(BigheadBtn, 6)

    BigheadBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "bighead " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        BigheadBtn.Text = "✔ تم!"
        _tw(BigheadBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if BigheadBtn and BigheadBtn.Parent then
                BigheadBtn.Text = "🗿  Bighead"
                _tw(BigheadBtn, {BackgroundColor3 = Color3.fromRGB(100,30,100)})
            end
        end)
    end)

    BigheadBtn.MouseEnter:Connect(function()  _tw(BigheadBtn, {BackgroundColor3=Color3.fromRGB(math.min(100+40,255),math.min(30+40,255),math.min(100+40,255))}) end)
    BigheadBtn.MouseLeave:Connect(function() _tw(BigheadBtn, {BackgroundColor3=Color3.fromRGB(100,30,100)}) end)
    
    local JumpBtn = Instance.new("TextButton", Card)
    JumpBtn.Size = UDim2.new(0.5,-12,0,28)
    JumpBtn.Position = UDim2.new(0,8,0,320)
    JumpBtn.BackgroundColor3 = Color3.fromRGB(30,100,160)
    JumpBtn.Text = "⬆️  Jump"
    JumpBtn.TextColor3 = SC.TEXT
    JumpBtn.TextSize = 11
    JumpBtn.Font = Enum.Font.GothamBold
    JumpBtn.BorderSizePixel = 0
    _corner(JumpBtn, 6)

    JumpBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "jump " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        JumpBtn.Text = "✔ تم!"
        _tw(JumpBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if JumpBtn and JumpBtn.Parent then
                JumpBtn.Text = "⬆️  Jump"
                _tw(JumpBtn, {BackgroundColor3 = Color3.fromRGB(30,100,160)})
            end
        end)
    end)

    JumpBtn.MouseEnter:Connect(function()  _tw(JumpBtn, {BackgroundColor3=Color3.fromRGB(math.min(30+40,255),math.min(100+40,255),math.min(160+40,255))}) end)
    JumpBtn.MouseLeave:Connect(function() _tw(JumpBtn, {BackgroundColor3=Color3.fromRGB(30,100,160)}) end)
    
    local HideguisBtn = Instance.new("TextButton", Card)
    HideguisBtn.Size = UDim2.new(0.5,-12,0,28)
    HideguisBtn.Position = UDim2.new(0.5,4,0,320)
    HideguisBtn.BackgroundColor3 = Color3.fromRGB(50,50,50)
    HideguisBtn.Text = "🙈  Hideguis"
    HideguisBtn.TextColor3 = SC.TEXT
    HideguisBtn.TextSize = 11
    HideguisBtn.Font = Enum.Font.GothamBold
    HideguisBtn.BorderSizePixel = 0
    _corner(HideguisBtn, 6)

    HideguisBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "hideguis " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        HideguisBtn.Text = "✔ تم!"
        _tw(HideguisBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if HideguisBtn and HideguisBtn.Parent then
                HideguisBtn.Text = "🙈  Hideguis"
                _tw(HideguisBtn, {BackgroundColor3 = Color3.fromRGB(50,50,50)})
            end
        end)
    end)

    HideguisBtn.MouseEnter:Connect(function()  _tw(HideguisBtn, {BackgroundColor3=Color3.fromRGB(math.min(50+40,255),math.min(50+40,255),math.min(50+40,255))}) end)
    HideguisBtn.MouseLeave:Connect(function() _tw(HideguisBtn, {BackgroundColor3=Color3.fromRGB(50,50,50)}) end)

    local InvisibleBtn = Instance.new("TextButton", Card)
    InvisibleBtn.Size = UDim2.new(0.5,-12,0,28)
    InvisibleBtn.Position = UDim2.new(0,8,0,352)
    InvisibleBtn.BackgroundColor3 = Color3.fromRGB(20, 20, 80)
    InvisibleBtn.Text = "👻  Invisible"
    InvisibleBtn.TextColor3 = SC.TEXT
    InvisibleBtn.TextSize = 11
    InvisibleBtn.Font = Enum.Font.GothamBold
    InvisibleBtn.BorderSizePixel = 0
    _corner(InvisibleBtn, 6)

    InvisibleBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "invisible " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        InvisibleBtn.Text = "✔ تم!"
        _tw(InvisibleBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if InvisibleBtn and InvisibleBtn.Parent then
                InvisibleBtn.Text = "👻  Invisible"
                _tw(InvisibleBtn, {BackgroundColor3 = Color3.fromRGB(20,20,80)})
            end
        end)
    end)

    InvisibleBtn.MouseEnter:Connect(function()  _tw(InvisibleBtn, {BackgroundColor3=Color3.fromRGB(40,40,120)}) end)
    InvisibleBtn.MouseLeave:Connect(function() _tw(InvisibleBtn, {BackgroundColor3=Color3.fromRGB(20,20,80)}) end)

    local SpeedBtn = Instance.new("TextButton", Card)
    SpeedBtn.Size = UDim2.new(1,-16,0,28)
    SpeedBtn.Position = UDim2.new(0,8,0,384)
    SpeedBtn.BackgroundColor3 = Color3.fromRGB(20, 100, 80)
    SpeedBtn.Text = "⚡  Speed 0"
    SpeedBtn.TextColor3 = SC.TEXT
    SpeedBtn.TextSize = 11
    SpeedBtn.Font = Enum.Font.GothamBold
    SpeedBtn.BorderSizePixel = 0
    _corner(SpeedBtn, 6)

    SpeedBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "speed " .. p.Name .. " 0"

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        SpeedBtn.Text = "✔ تم!"
        _tw(SpeedBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if SpeedBtn and SpeedBtn.Parent then
                SpeedBtn.Text = "⚡  Speed 0"
                _tw(SpeedBtn, {BackgroundColor3 = Color3.fromRGB(20,100,80)})
            end
        end)
    end)

    SpeedBtn.MouseEnter:Connect(function()  _tw(SpeedBtn, {BackgroundColor3=Color3.fromRGB(30,150,120)}) end)
    SpeedBtn.MouseLeave:Connect(function() _tw(SpeedBtn, {BackgroundColor3=Color3.fromRGB(20,100,80)}) end)

    local ScanUnInvisBtn = Instance.new("TextButton", Card)
    ScanUnInvisBtn.Size = UDim2.new(0.5,-12,0,28)
    ScanUnInvisBtn.Position = UDim2.new(0.5,4,0,352)
    ScanUnInvisBtn.BackgroundColor3 = Color3.fromRGB(20, 20, 80)
    ScanUnInvisBtn.Text = "👁️  Uninvisible"
    ScanUnInvisBtn.TextColor3 = SC.TEXT
    ScanUnInvisBtn.TextSize = 11
    ScanUnInvisBtn.Font = Enum.Font.GothamBold
    ScanUnInvisBtn.BorderSizePixel = 0
    _corner(ScanUnInvisBtn, 6)

    ScanUnInvisBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "uninvisible " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        ScanUnInvisBtn.Text = "✔ تم!"
        _tw(ScanUnInvisBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if ScanUnInvisBtn and ScanUnInvisBtn.Parent then
                ScanUnInvisBtn.Text = "👁️  Uninvisible"
                _tw(ScanUnInvisBtn, {BackgroundColor3 = Color3.fromRGB(20,20,80)})
            end
        end)
    end)

    ScanUnInvisBtn.MouseEnter:Connect(function()  _tw(ScanUnInvisBtn, {BackgroundColor3=Color3.fromRGB(40,40,120)}) end)
    ScanUnInvisBtn.MouseLeave:Connect(function() _tw(ScanUnInvisBtn, {BackgroundColor3=Color3.fromRGB(20,20,80)}) end)
    
    local FlyBtn = Instance.new("TextButton", Card)
    FlyBtn.Size = UDim2.new(0.5,-12,0,28)
    FlyBtn.Position = UDim2.new(0,8,0,416)
    FlyBtn.BackgroundColor3 = Color3.fromRGB(20, 80, 20)
    FlyBtn.Text = "🕊️  Fly"
    FlyBtn.TextColor3 = SC.TEXT
    FlyBtn.TextSize = 11
    FlyBtn.Font = Enum.Font.GothamBold
    FlyBtn.BorderSizePixel = 0
    _corner(FlyBtn, 6)

    FlyBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "fly " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
        task.wait(0.05)
        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        FlyBtn.Text = "✔ تم!"
        _tw(FlyBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if FlyBtn and FlyBtn.Parent then
                FlyBtn.Text = "🕊️  Fly"
                _tw(FlyBtn, {BackgroundColor3 = Color3.fromRGB(20,80,20)})
            end
        end)
    end)

    FlyBtn.MouseEnter:Connect(function()  _tw(FlyBtn, {BackgroundColor3=Color3.fromRGB(40,120,40)}) end)
    FlyBtn.MouseLeave:Connect(function() _tw(FlyBtn, {BackgroundColor3=Color3.fromRGB(20,80,20)}) end)

    local UnflyBtn = Instance.new("TextButton", Card)
    UnflyBtn.Size = UDim2.new(0.5,-12,0,28)
    UnflyBtn.Position = UDim2.new(0.5,4,0,416)
    UnflyBtn.BackgroundColor3 = Color3.fromRGB(80, 20, 20)
    UnflyBtn.Text = "🔻  Unfly"
    UnflyBtn.TextColor3 = SC.TEXT
    UnflyBtn.TextSize = 11
    UnflyBtn.Font = Enum.Font.GothamBold
    UnflyBtn.BorderSizePixel = 0
    _corner(UnflyBtn, 6)

    UnflyBtn.MouseButton1Click:Connect(function()
        local vim = game:GetService("VirtualInputManager")
        local UIS = game:GetService("UserInputService")
        local full = "unfly " .. p.Name

        vim:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)

        local cmdBox = UIS:GetFocusedTextBox()
        if cmdBox then
            cmdBox.Text = cmdBox.Text .. full
            cmdBox.CursorPosition = #cmdBox.Text + 1
        end
        task.wait(0.05)

        vim:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim:SendKeyEvent(false, Enum.KeyCode.Return, false, game)

        UnflyBtn.Text = "✔ تم!"
        _tw(UnflyBtn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if UnflyBtn and UnflyBtn.Parent then
                UnflyBtn.Text = "🔻  Unfly"
                _tw(UnflyBtn, {BackgroundColor3 = Color3.fromRGB(80,20,20)})
            end
        end)
    end)

    UnflyBtn.MouseEnter:Connect(function()  _tw(UnflyBtn, {BackgroundColor3=Color3.fromRGB(120,40,40)}) end)
    UnflyBtn.MouseLeave:Connect(function() _tw(UnflyBtn, {BackgroundColor3=Color3.fromRGB(80,20,20)}) end)

    local function _fireTitle(titleText, btn, origText, origColor)
        local vim_ = game:GetService("VirtualInputManager")
        local UIS_ = game:GetService("UserInputService")
        local full_ = "title " .. p.Name .. " " .. titleText
        vim_:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
        vim_:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
        task.wait(0.2)
        local cb = UIS_:GetFocusedTextBox()
        if cb then
            cb.Text = cb.Text .. full_
            cb.CursorPosition = #cb.Text + 1
        end
        task.wait(0.05)
        vim_:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
        vim_:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
        btn.Text = "✔ تم!"
        _tw(btn, {BackgroundColor3 = SC.GREEN})
        task.delay(1.5, function()
            if btn and btn.Parent then
                btn.Text = origText
                _tw(btn, {BackgroundColor3 = origColor})
            end
        end)
    end

    local KalbBtn = Instance.new("TextButton", Card)
    KalbBtn.Size             = UDim2.new(0.5,-12,0,28)
    KalbBtn.Position         = UDim2.new(0,8,0,452)
    KalbBtn.BackgroundColor3 = Color3.fromRGB(170, 50, 50)
    KalbBtn.Text             = "🐕 انا كلب"
    KalbBtn.TextColor3       = SC.TEXT
    KalbBtn.TextSize         = 11
    KalbBtn.Font             = Enum.Font.GothamBold
    KalbBtn.BorderSizePixel  = 0
    _corner(KalbBtn, 6)
    KalbBtn.MouseButton1Click:Connect(function()
        
        local vim_ = game:GetService("VirtualInputManager")
        local UIS_ = game:GetService("UserInputService")

        local function _sendCmd(cmdText)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
            task.wait(0.2)
            local cb = UIS_:GetFocusedTextBox()
            if cb then
                cb.Text = cb.Text .. cmdText
                cb.CursorPosition = #cb.Text + 1
            end
            task.wait(0.05)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
            task.wait(0.4)
        end

        KalbBtn.Text = "⏳ جاري..."
        _tw(KalbBtn, {BackgroundColor3 = Color3.fromRGB(80,80,80)})

        task.spawn(function()
            _sendCmd("dog " .. p.Name)               
            _sendCmd("neon "    .. p.Name)           
            _sendCmd("title "   .. p.Name .. " انا كلب") 

            KalbBtn.Text = "✔ تم!"
            _tw(KalbBtn, {BackgroundColor3 = SC.GREEN})
            task.delay(2, function()
                if KalbBtn and KalbBtn.Parent then
                    KalbBtn.Text = "🐕 انا كلب"
                    _tw(KalbBtn, {BackgroundColor3 = Color3.fromRGB(170,50,50)})
                end
            end)
        end)
    end)
    KalbBtn.MouseEnter:Connect(function()  _tw(KalbBtn, {BackgroundColor3=Color3.fromRGB(210,70,70)}) end)
    KalbBtn.MouseLeave:Connect(function() _tw(KalbBtn, {BackgroundColor3=Color3.fromRGB(170,50,50)}) end)

    local QahbaBtn = Instance.new("TextButton", Card)
    QahbaBtn.Size             = UDim2.new(0.5,-12,0,28)
    QahbaBtn.Position         = UDim2.new(0.5,4,0,452)
    QahbaBtn.BackgroundColor3 = Color3.fromRGB(120, 30, 150)
    QahbaBtn.Text             = "💜 قـ.حـ.به السيرفر"
    QahbaBtn.TextColor3       = SC.TEXT
    QahbaBtn.TextSize         = 10
    QahbaBtn.Font             = Enum.Font.GothamBold
    QahbaBtn.BorderSizePixel  = 0
    _corner(QahbaBtn, 6)
    QahbaBtn.MouseButton1Click:Connect(function()
        
        local vim_ = game:GetService("VirtualInputManager")
        local UIS_ = game:GetService("UserInputService")

        local function _sendCmd(cmdText)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
            task.wait(0.2)
            local cb = UIS_:GetFocusedTextBox()
            if cb then
                cb.Text = cb.Text .. cmdText
                cb.CursorPosition = #cb.Text + 1
            end
            task.wait(0.05)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
            task.wait(0.4)
        end

        QahbaBtn.Text = "⏳ جاري..."
        _tw(QahbaBtn, {BackgroundColor3 = Color3.fromRGB(80,80,80)})

        task.spawn(function()
            _sendCmd("wormify " .. p.Name)                          
            _sendCmd("neon "    .. p.Name)                          
            _sendCmd("title "   .. p.Name .. " انا قـ.حـ.به السيرفر") 

            QahbaBtn.Text = "✔ تم!"
            _tw(QahbaBtn, {BackgroundColor3 = SC.GREEN})
            task.delay(2, function()
                if QahbaBtn and QahbaBtn.Parent then
                    QahbaBtn.Text = "💜 قـ.حـ.به السيرفر"
                    _tw(QahbaBtn, {BackgroundColor3 = Color3.fromRGB(120,30,150)})
                end
            end)
        end)
    end)
    QahbaBtn.MouseEnter:Connect(function()  _tw(QahbaBtn, {BackgroundColor3=Color3.fromRGB(160,50,190)}) end)
    QahbaBtn.MouseLeave:Connect(function() _tw(QahbaBtn, {BackgroundColor3=Color3.fromRGB(120,30,150)}) end)
    local KharqiBtn = Instance.new("TextButton", Card)
    KharqiBtn.Size             = UDim2.new(0.5,-12,0,28)
    KharqiBtn.Position         = UDim2.new(0,8,0,486)
    KharqiBtn.BackgroundColor3 = Color3.fromRGB(160, 80, 0)
    KharqiBtn.Text             = "🔥 خـ.رقي يـ.حـ.كـ.ني"
    KharqiBtn.TextColor3       = SC.TEXT
    KharqiBtn.TextSize         = 10
    KharqiBtn.Font             = Enum.Font.GothamBold
    KharqiBtn.BorderSizePixel  = 0
    _corner(KharqiBtn, 6)
    KharqiBtn.MouseButton1Click:Connect(function()
        local vim_ = game:GetService("VirtualInputManager")
        local UIS_ = game:GetService("UserInputService")

        local function _sendCmd(cmdText)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
            task.wait(0.1)
            local cb = UIS_:GetFocusedTextBox()
            if cb then
                cb.Text = cb.Text .. cmdText
                cb.CursorPosition = #cb.Text + 1
            end
            task.wait(0.05)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
            task.wait(0.2)
        end

        KharqiBtn.Text = "⏳ جاري..."
        _tw(KharqiBtn, {BackgroundColor3 = Color3.fromRGB(80,80,80)})

        task.spawn(function()
            _sendCmd("bigify " .. p.Name)                                  
            _sendCmd("neon "   .. p.Name)                                  
            _sendCmd("color "  .. p.Name .. " pink")                       
            _sendCmd("dog "    .. p.Name)                                  
            _sendCmd("speed "  .. p.Name .. " 0")                          
            _sendCmd("title "  .. p.Name .. " خـ.رقي يـ.حـ.كـ.ني")        

            KharqiBtn.Text = "✔ تم!"
            _tw(KharqiBtn, {BackgroundColor3 = SC.GREEN})
            task.delay(2, function()
                if KharqiBtn and KharqiBtn.Parent then
                    KharqiBtn.Text = "🔥 خـ.رقي يـ.حـ.كـ.ني"
                    _tw(KharqiBtn, {BackgroundColor3 = Color3.fromRGB(160,80,0)})
                end
            end)
        end)
    end)
    KharqiBtn.MouseEnter:Connect(function()  _tw(KharqiBtn, {BackgroundColor3=Color3.fromRGB(200,110,0)}) end)
    KharqiBtn.MouseLeave:Connect(function() _tw(KharqiBtn, {BackgroundColor3=Color3.fromRGB(160,80,0)}) end)

    local YnekBtn = Instance.new("TextButton", Card)
    YnekBtn.Size             = UDim2.new(0.5,-12,0,28)
    YnekBtn.Position         = UDim2.new(0.5,4,0,486)
    YnekBtn.BackgroundColor3 = Color3.fromRGB(30, 100, 30)
    YnekBtn.Text             = "💚 ابي احد يـ.نــ.يــ.كــ.ني"
    YnekBtn.TextColor3       = SC.TEXT
    YnekBtn.TextSize         = 10
    YnekBtn.Font             = Enum.Font.GothamBold
    YnekBtn.BorderSizePixel  = 0
    _corner(YnekBtn, 6)
    YnekBtn.MouseButton1Click:Connect(function()
        _fireTitle("ابي احد يـ.نــ.يــ.كــ.ني", YnekBtn, "💚 ابي احد يـ.نــ.يــ.كــ.ني", Color3.fromRGB(30,100,30))
    end)
    YnekBtn.MouseEnter:Connect(function()  _tw(YnekBtn, {BackgroundColor3=Color3.fromRGB(50,140,50)}) end)
    YnekBtn.MouseLeave:Connect(function() _tw(YnekBtn, {BackgroundColor3=Color3.fromRGB(30,100,30)}) end)

    local MamhoonBtn = Instance.new("TextButton", Card)
    MamhoonBtn.Size             = UDim2.new(1,-16,0,28)
    MamhoonBtn.Position         = UDim2.new(0,8,0,520)
    MamhoonBtn.BackgroundColor3 = Color3.fromRGB(160, 0, 120)
    MamhoonBtn.Text             = "🔥 انا مـ.ـمـ.ـ.حـــ.ـ.ون"
    MamhoonBtn.TextColor3       = SC.TEXT
    MamhoonBtn.TextSize         = 11
    MamhoonBtn.Font             = Enum.Font.GothamBold
    MamhoonBtn.BorderSizePixel  = 0
    _corner(MamhoonBtn, 6)
    MamhoonBtn.MouseButton1Click:Connect(function()
        local vim_ = game:GetService("VirtualInputManager")
        local UIS_ = game:GetService("UserInputService")

        local function _sendCmd(cmdText)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
            task.wait(0.1)
            local cb = UIS_:GetFocusedTextBox()
            if cb then
                cb.Text = cb.Text .. cmdText
                cb.CursorPosition = #cb.Text + 1
            end
            task.wait(0.05)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
            task.wait(0.2)
        end

        MamhoonBtn.Text = "⏳ جاري..."
        _tw(MamhoonBtn, {BackgroundColor3 = Color3.fromRGB(80,80,80)})

        task.spawn(function()
            _sendCmd("bigify " .. p.Name)                               
            _sendCmd("neon "   .. p.Name)                               
            _sendCmd("dog "    .. p.Name)                               
            _sendCmd("speed "  .. p.Name .. " 0")                       
            _sendCmd("title "  .. p.Name .. " انا مـ.ـمـ.ـ.حـــ.ـ.ون")  

            MamhoonBtn.Text = "✔ تم!"
            _tw(MamhoonBtn, {BackgroundColor3 = SC.GREEN})
            task.delay(2, function()
                if MamhoonBtn and MamhoonBtn.Parent then
                    MamhoonBtn.Text = "🔥 انا مـ.ـمـ.ـ.حـــ.ـ.ون"
                    _tw(MamhoonBtn, {BackgroundColor3 = Color3.fromRGB(160,0,120)})
                end
            end)
        end)
    end)
    MamhoonBtn.MouseEnter:Connect(function()  _tw(MamhoonBtn, {BackgroundColor3=Color3.fromRGB(200,0,160)}) end)
    MamhoonBtn.MouseLeave:Connect(function() _tw(MamhoonBtn, {BackgroundColor3=Color3.fromRGB(160,0,120)}) end)

    local spamActive = false
    game:GetService("Players").PlayerRemoving:Connect(function(leavingPlayer)
        if leavingPlayer == p and spamActive then
            spamActive = false
            SpamBtn.Text = "🔴 سبام"
            _tw(SpamBtn, {BackgroundColor3 = Color3.fromRGB(150,0,0)})
        end
    end)
    local SpamBtn = Instance.new("TextButton", Card)
    SpamBtn.Size             = UDim2.new(1,-16,0,28)
    SpamBtn.Position         = UDim2.new(0,8,0,558)
    SpamBtn.BackgroundColor3 = Color3.fromRGB(150, 0, 0)
    SpamBtn.Text             = "🔴 سبام"
    SpamBtn.TextColor3       = SC.TEXT
    SpamBtn.TextSize         = 11
    SpamBtn.Font             = Enum.Font.GothamBold
    SpamBtn.BorderSizePixel  = 0
    _corner(SpamBtn, 6)
    SpamBtn.MouseButton1Click:Connect(function()
        if spamActive then
            spamActive = false
            SpamBtn.Text = "🔴 سبام"
            _tw(SpamBtn, {BackgroundColor3 = Color3.fromRGB(150,0,0)})
        else
            spamActive = true
            SpamBtn.Text = "✅ سبام (شغال)"
            _tw(SpamBtn, {BackgroundColor3 = Color3.fromRGB(0,140,0)})
            task.spawn(function()
                local vim_ = game:GetService("VirtualInputManager")
                local UIS_ = game:GetService("UserInputService")
                local function _sendCmd(cmdText)
                    vim_:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
                    vim_:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
                    task.wait(0.05)
                    local cb = UIS_:GetFocusedTextBox()
                    if cb then
                        cb.Text = cb.Text .. cmdText
                        cb.CursorPosition = #cb.Text + 1
                    end
                    task.wait(0.03)
                    vim_:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
                    vim_:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
                    task.wait(0.7)
                end
                while spamActive do
                    for i = 1, 10 do
                        if not spamActive then break end
                        _sendCmd("laserEyes " .. p.Name)  
                        _sendCmd("laserEyes " .. p.Name)
                        _sendCmd("laserEyes " .. p.Name)
                        _sendCmd("laserEyes " .. p.Name)
                        _sendCmd("laserEyes " .. p.Name)
                        _sendCmd("laserEyes " .. p.Name)
                        if not spamActive then break end
                        _sendCmd("ping "      .. p.Name)  
                        _sendCmd("ping "      .. p.Name)
                        _sendCmd("ping "      .. p.Name)
                        _sendCmd("ping "      .. p.Name)
                    end
                    if not spamActive then break end
                    task.wait(2)
                end
            end)
        end
    end)
    SpamBtn.MouseEnter:Connect(function()
        if not spamActive then _tw(SpamBtn, {BackgroundColor3=Color3.fromRGB(190,0,0)}) end
    end)
    SpamBtn.MouseLeave:Connect(function()
        if not spamActive then _tw(SpamBtn, {BackgroundColor3=Color3.fromRGB(150,0,0)}) end
    end)
    
    local FullTrollBtn = Instance.new("TextButton", Card)
    FullTrollBtn.Size             = UDim2.new(0.5,-12,0,28)
    FullTrollBtn.Position         = UDim2.new(0,8,0,596)
    FullTrollBtn.BackgroundColor3 = Color3.fromRGB(180, 0, 100)
    FullTrollBtn.Text             = "🎭 Full Troll"
    FullTrollBtn.TextColor3       = SC.TEXT
    FullTrollBtn.TextSize         = 11
    FullTrollBtn.Font             = Enum.Font.GothamBold
    FullTrollBtn.BorderSizePixel  = 0
    _corner(FullTrollBtn, 6)
    FullTrollBtn.MouseButton1Click:Connect(function()
        local vim_ = game:GetService("VirtualInputManager")
        local UIS_ = game:GetService("UserInputService")

        local function _sendCmd(cmdText)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
            task.wait(0.2)
            local cb = UIS_:GetFocusedTextBox()
            if cb then
                cb.Text = cb.Text .. cmdText
                cb.CursorPosition = #cb.Text + 1
            end
            task.wait(0.05)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
            task.wait(0.4)
        end

        FullTrollBtn.Text = "⏳ جاري..."
        _tw(FullTrollBtn, {BackgroundColor3 = Color3.fromRGB(80,80,80)})

        task.spawn(function()
            _sendCmd("squash "  .. p.Name)                  
            _sendCmd("aura "    .. p.Name)                  
            _sendCmd("bigHead " .. p.Name)                  
            _sendCmd("ghost "   .. p.Name)                  
            _sendCmd("shine "   .. p.Name)                  
            _sendCmd("speed "   .. p.Name .. " 0")          
            _sendCmd("titlepk " .. p.Name .. " hhh")         
            _sendCmd("color "   .. p.Name .. " pink")       

            FullTrollBtn.Text = "✔ تم!"
            _tw(FullTrollBtn, {BackgroundColor3 = SC.GREEN})
            task.delay(2, function()
                if FullTrollBtn and FullTrollBtn.Parent then
                    FullTrollBtn.Text = "🎭 Full Troll"
                    _tw(FullTrollBtn, {BackgroundColor3 = Color3.fromRGB(180,0,100)})
                end
            end)
        end)
    end)
    FullTrollBtn.MouseEnter:Connect(function()  _tw(FullTrollBtn, {BackgroundColor3=Color3.fromRGB(220,0,130)}) end)
    FullTrollBtn.MouseLeave:Connect(function() _tw(FullTrollBtn, {BackgroundColor3=Color3.fromRGB(180,0,100)}) end)

    local FullTroll2Btn = Instance.new("TextButton", Card)
    FullTroll2Btn.Size             = UDim2.new(0.5,-12,0,28)
    FullTroll2Btn.Position         = UDim2.new(0.5,4,0,596)
    FullTroll2Btn.BackgroundColor3 = Color3.fromRGB(100, 0, 160)
    FullTroll2Btn.Text             = "🎭 Full Troll 2"
    FullTroll2Btn.TextColor3       = SC.TEXT
    FullTroll2Btn.TextSize         = 11
    FullTroll2Btn.Font             = Enum.Font.GothamBold
    FullTroll2Btn.BorderSizePixel  = 0
    _corner(FullTroll2Btn, 6)
    FullTroll2Btn.MouseButton1Click:Connect(function()
        local vim_ = game:GetService("VirtualInputManager")
        local UIS_ = game:GetService("UserInputService")

        local function _sendCmd(cmdText)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
            task.wait(0.2)
            local cb = UIS_:GetFocusedTextBox()
            if cb then
                cb.Text = cb.Text .. cmdText
                cb.CursorPosition = #cb.Text + 1
            end
            task.wait(0.05)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
            task.wait(0.4)
        end

        FullTroll2Btn.Text = "⏳ جاري..."
        _tw(FullTroll2Btn, {BackgroundColor3 = Color3.fromRGB(80,80,80)})

        task.spawn(function()
            _sendCmd("bigHead "  .. p.Name)              
            _sendCmd("squash "   .. p.Name)              
            _sendCmd("shine "    .. p.Name .. " 0")      
            _sendCmd("noclip "   .. p.Name .. " 0")      
            _sendCmd("sit "      .. p.Name)              
            _sendCmd("titlepk "  .. p.Name .. " hhh")    
            _sendCmd("color "    .. p.Name .. " pink")   

            FullTroll2Btn.Text = "✔ تم!"
            _tw(FullTroll2Btn, {BackgroundColor3 = SC.GREEN})
            task.delay(2, function()
                if FullTroll2Btn and FullTroll2Btn.Parent then
                    FullTroll2Btn.Text = "🎭 Full Troll 2"
                    _tw(FullTroll2Btn, {BackgroundColor3 = Color3.fromRGB(100,0,160)})
                end
            end)
        end)
    end)
    FullTroll2Btn.MouseEnter:Connect(function()  _tw(FullTroll2Btn, {BackgroundColor3=Color3.fromRGB(130,0,200)}) end)
    FullTroll2Btn.MouseLeave:Connect(function() _tw(FullTroll2Btn, {BackgroundColor3=Color3.fromRGB(100,0,160)}) end)

    local FullTroll3Btn = Instance.new("TextButton", Card)
    FullTroll3Btn.Size             = UDim2.new(0.5,-12,0,28)
    FullTroll3Btn.Position         = UDim2.new(0,8,0,628)
    FullTroll3Btn.BackgroundColor3 = Color3.fromRGB(0, 120, 80)
    FullTroll3Btn.Text             = "🎭 Full Troll 3"
    FullTroll3Btn.TextColor3       = SC.TEXT
    FullTroll3Btn.TextSize         = 11
    FullTroll3Btn.Font             = Enum.Font.GothamBold
    FullTroll3Btn.BorderSizePixel  = 0
    _corner(FullTroll3Btn, 6)
    FullTroll3Btn.MouseButton1Click:Connect(function()
        local vim_ = game:GetService("VirtualInputManager")
        local UIS_ = game:GetService("UserInputService")

        local function _sendCmd(cmdText)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
            task.wait(0.2)
            local cb = UIS_:GetFocusedTextBox()
            if cb then
                cb.Text = cb.Text .. cmdText
                cb.CursorPosition = #cb.Text + 1
            end
            task.wait(0.05)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
            task.wait(0.4)
        end

        FullTroll3Btn.Text = "⏳ جاري..."
        _tw(FullTroll3Btn, {BackgroundColor3 = Color3.fromRGB(80,80,80)})

        task.spawn(function()
            _sendCmd("aura "    .. p.Name)               
            _sendCmd("wormify " .. p.Name)               
            _sendCmd("size "    .. p.Name .. " 3")       
            _sendCmd("titlepk " .. p.Name .. " hhh")     
            _sendCmd("ghost "   .. p.Name)               
            _sendCmd("color "   .. p.Name .. " pink")    

            FullTroll3Btn.Text = "✔ تم!"
            _tw(FullTroll3Btn, {BackgroundColor3 = SC.GREEN})
            task.delay(2, function()
                if FullTroll3Btn and FullTroll3Btn.Parent then
                    FullTroll3Btn.Text = "🎭 Full Troll 3"
                    _tw(FullTroll3Btn, {BackgroundColor3 = Color3.fromRGB(0,120,80)})
                end
            end)
        end)
    end)
    FullTroll3Btn.MouseEnter:Connect(function()  _tw(FullTroll3Btn, {BackgroundColor3=Color3.fromRGB(0,160,110)}) end)
    FullTroll3Btn.MouseLeave:Connect(function() _tw(FullTroll3Btn, {BackgroundColor3=Color3.fromRGB(0,120,80)}) end)

    local FullTroll4Btn = Instance.new("TextButton", Card)
    FullTroll4Btn.Size             = UDim2.new(0.5,-12,0,28)
    FullTroll4Btn.Position         = UDim2.new(0.5,4,0,628)
    FullTroll4Btn.BackgroundColor3 = Color3.fromRGB(160, 80, 0)
    FullTroll4Btn.Text             = "🎭 Full Troll 4"
    FullTroll4Btn.TextColor3       = SC.TEXT
    FullTroll4Btn.TextSize         = 11
    FullTroll4Btn.Font             = Enum.Font.GothamBold
    FullTroll4Btn.BorderSizePixel  = 0
    _corner(FullTroll4Btn, 6)
    FullTroll4Btn.MouseButton1Click:Connect(function()
        local vim_ = game:GetService("VirtualInputManager")
        local UIS_ = game:GetService("UserInputService")

        local function _sendCmd(cmdText)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Quote, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Quote, false, game)
            task.wait(0.2)
            local cb = UIS_:GetFocusedTextBox()
            if cb then
                cb.Text = cb.Text .. cmdText
                cb.CursorPosition = #cb.Text + 1
            end
            task.wait(0.05)
            vim_:SendKeyEvent(true,  Enum.KeyCode.Return, false, game)
            vim_:SendKeyEvent(false, Enum.KeyCode.Return, false, game)
            task.wait(0.4)
        end

        FullTroll4Btn.Text = "⏳ جاري..."
        _tw(FullTroll4Btn, {BackgroundColor3 = Color3.fromRGB(80,80,80)})

        task.spawn(function()
            _sendCmd("ratDance " .. p.Name)              
            _sendCmd("squash "   .. p.Name)              
            _sendCmd("bigHead "  .. p.Name)              
            _sendCmd("ghost "    .. p.Name)              
            _sendCmd("titlepk "  .. p.Name .. " hhh")    
            _sendCmd("color "    .. p.Name .. " pink")   

            FullTroll4Btn.Text = "✔ تم!"
            _tw(FullTroll4Btn, {BackgroundColor3 = SC.GREEN})
            task.delay(2, function()
                if FullTroll4Btn and FullTroll4Btn.Parent then
                    FullTroll4Btn.Text = "🎭 Full Troll 4"
                    _tw(FullTroll4Btn, {BackgroundColor3 = Color3.fromRGB(160,80,0)})
                end
            end)
        end)
    end)
    FullTroll4Btn.MouseEnter:Connect(function()  _tw(FullTroll4Btn, {BackgroundColor3=Color3.fromRGB(200,110,0)}) end)
    FullTroll4Btn.MouseLeave:Connect(function() _tw(FullTroll4Btn, {BackgroundColor3=Color3.fromRGB(160,80,0)}) end)

    local trollBtns = {TitleBtn, NameBtn, KalbBtn, QahbaBtn, KharqiBtn, YnekBtn, MamhoonBtn, SpamBtn, FullTrollBtn, FullTroll2Btn, FullTroll3Btn, FullTroll4Btn, DogBtn, ViewBtn, UnviewBtn, RespawnBtn, TakeLBtn, ChibifyBtn,
                        FreakifyBtn, BigifyBtn, FatifyBtn, NeonBtn, GoldBtn,
                        BigheadBtn, JumpBtn, HideguisBtn, InvisibleBtn, SpeedBtn, ScanUnInvisBtn, FlyBtn, UnflyBtn}

    local trollOpen = _trollOpenSet[p.Name] or false

    local function applyTrollState()
        for _, b in pairs(trollBtns) do b.Visible = trollOpen end
        Card.Size = UDim2.new(1,0,0, trollOpen and 682 or 100)
        TrollBtn.Text = trollOpen and "🎭 ترول ▲" or "🎭 ترول ▼"
        TrollBtn.BackgroundColor3 = trollOpen and Color3.fromRGB(120,50,180) or Color3.fromRGB(80,30,120)
    end

    applyTrollState()

    TrollBtn.MouseButton1Click:Connect(function()
        trollOpen = not trollOpen
        _trollOpenSet[p.Name] = trollOpen  
        applyTrollState()
    end)

    TrollBtn.MouseEnter:Connect(function()  _tw(TrollBtn, {BackgroundColor3=Color3.fromRGB(120,50,180)}) end)
    TrollBtn.MouseLeave:Connect(function()
        if not trollOpen then _tw(TrollBtn, {BackgroundColor3=Color3.fromRGB(80,30,120)}) end
    end)
end

local _stableOrder = {}  

local function _refreshStableOrder()
    local existing = {}
    for _, name in ipairs(_stableOrder) do existing[name] = true end
    
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LocalPlayer and not existing[p.Name] then
            table.insert(_stableOrder, p.Name)
        end
    end
    
    local current = {}
    for _, p in ipairs(Players:GetPlayers()) do current[p.Name] = true end
    local filtered = {}
    for _, name in ipairs(_stableOrder) do
        if current[name] then table.insert(filtered, name) end
    end
    _stableOrder = filtered
end

local function doScan()
    _refreshStableOrder()
    local myRoot = GetRoot()
    local list = {}
    if sortByDist then
        for _, p in ipairs(Players:GetPlayers()) do
            if p ~= LocalPlayer then table.insert(list, p) end
        end
        table.sort(list, function(a, b)
            local ra = _getRoot2(a); local rb = _getRoot2(b)
            local da = (ra and myRoot) and (ra.Position-myRoot.Position).Magnitude or math.huge
            local db = (rb and myRoot) and (rb.Position-myRoot.Position).Magnitude or math.huge
            return da < db
        end)
    else
        local playerMap = {}
        for _, p in ipairs(Players:GetPlayers()) do playerMap[p.Name] = p end
        
        if _pinnedPlayer and playerMap[_pinnedPlayer] then
            table.insert(list, playerMap[_pinnedPlayer])
        end
        for _, name in ipairs(_stableOrder) do
            if playerMap[name] and name ~= _pinnedPlayer then
                table.insert(list, playerMap[name])
            end
        end
    end
    CountLbl.Text = "اللاعبون: "..#list

    local existingCards = {}
    for _, c in pairs(PlayerList:GetChildren()) do
        if c:IsA("Frame") then
            local pname = c:GetAttribute("PlayerName")
            if pname then existingCards[pname] = c end
        end
    end

    local currentNames = {}
    for _, p in ipairs(list) do currentNames[p.Name] = true end
    for name, card in pairs(existingCards) do
        if not currentNames[name] then
            _trollOpenSet[name] = nil
            card:Destroy()
        end
    end

    for i, p in ipairs(list) do
        if existingCards[p.Name] then
            existingCards[p.Name].LayoutOrder = i  
        else
            buildCard(p, i)
        end
    end

    _tw(ScanBtn, {BackgroundColor3=SC.ACCENT})
    task.delay(0.4, function() _tw(ScanBtn, {BackgroundColor3=SC.GREEN}) end)
end

local function applySettingsToChar(char)
    local _hum = char:WaitForChild("Humanoid", 10)
    if _hum then
        _hum.WalkSpeed = _currentSpeed
        _hum.JumpPower = _currentJump
    end
    workspace.Gravity = _currentGravity
end

task.spawn(function()
    task.wait(2) 

    local _char = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
    applySettingsToChar(_char)

    NoclipActive = true
    if not NoclipConn then
        NoclipConn = RunService.Stepped:Connect(function()
            if not NoclipActive then return end
            local c = GetChar()
            if c then
                for _, p in pairs(c:GetDescendants()) do
                    if p:IsA("BasePart") then p.CanCollide = false end
                end
            end
        end)
    end

    ESP.Active = true
    for _, p in pairs(Players:GetPlayers()) do
        BuildESP(p)
    end
end)

LocalPlayer.CharacterAdded:Connect(function(char)
    applySettingsToChar(char)
    
    if NoclipActive and not NoclipConn then
        NoclipConn = RunService.Stepped:Connect(function()
            if not NoclipActive then return end
            local c = GetChar()
            if c then
                for _, p in pairs(c:GetDescendants()) do
                    if p:IsA("BasePart") then p.CanCollide = false end
                end
            end
        end)
    end
end)

Players.PlayerAdded:Connect(function(p)
    spawnNotif(p.DisplayName.." (@"..p.Name..")  دخل السيرفر", true, p.UserId)
    task.delay(1.5, doScan)
end)
Players.PlayerRemoving:Connect(function(p)
    spawnNotif(p.DisplayName.." (@"..p.Name..")  خرج من السيرفر", false, p.UserId)
    task.delay(0.3, doScan)
end)

ScanBtn.MouseButton1Click:Connect(doScan)
task.delay(0.5, doScan)

Mouse.Button1Down:Connect(function()
    local target = Mouse.Target
    if not target or not target.Parent then return end
    for _, plr in pairs(Players:GetPlayers()) do
        if plr ~= LocalPlayer and plr.Character
           and target:IsDescendantOf(plr.Character) then
            _pinnedPlayer = plr.Name
            
            local rank = 1
            for _, card in pairs(PlayerList:GetChildren()) do
                if card:IsA("Frame") then
                    if card:GetAttribute("PlayerName") == plr.Name then
                        card.LayoutOrder = 0
                    else
                        card.LayoutOrder = rank
                        rank = rank + 1
                    end
                end
            end
            spawnNotif("📌 "..plr.DisplayName.." في أول القائمة", true)
            return
        end
    end
end)
task.spawn(function()
    while ScreenGui and ScreenGui.Parent do
        task.wait(5); doScan()
    end
end)

local HubTeleportService = game:GetService("TeleportService")
local HubHttpService     = game:GetService("HttpService")
local HUB_PLACE_ID       = game.PlaceId
local hubServerCache     = {}
local hubIsFetching      = false
local hubStatusLabel     = nil
local hubCardContainer   = nil

local function MakeHubToolBtn(parent, txt, w)
    local b = Instance.new("TextButton", parent)
    b.Size             = UDim2.new(0, w, 0, 26)
    b.BackgroundColor3 = Color3.fromRGB(100, 60, 220)
    b.TextColor3       = Color3.fromRGB(255, 255, 255)
    b.Text             = txt
    b.Font             = Enum.Font.GothamBold
    b.TextSize         = 12
    b.BorderSizePixel  = 0
    b.AutoButtonColor  = true
    Instance.new("UICorner", b).CornerRadius = UDim.new(0, 6)
    return b
end

local function HubClearCards()
    if not hubCardContainer then return end
    for _, c in pairs(hubCardContainer:GetChildren()) do
        if c:IsA("Frame") then c:Destroy() end
    end
end

local function HubMakeCard(srv, idx)
    local isCurrent = srv.id == game.JobId
    local isFull    = srv.playing >= srv.maxPlayers

    local Card = Instance.new("Frame", hubCardContainer)
    Card.Size             = UDim2.new(0, 510, 0, 54)
    Card.BackgroundColor3 = isCurrent and Color3.fromRGB(40,60,30) or Color3.fromRGB(28,28,42)
    Card.BorderSizePixel  = 0
    Card.LayoutOrder      = idx
    Instance.new("UICorner", Card).CornerRadius = UDim.new(0, 8)

    local BarBG = Instance.new("Frame", Card)
    BarBG.Size             = UDim2.new(1, -16, 0, 4)
    BarBG.Position         = UDim2.new(0, 8, 1, -8)
    BarBG.BackgroundColor3 = Color3.fromRGB(45, 45, 65)
    BarBG.BorderSizePixel  = 0
    Instance.new("UICorner", BarBG).CornerRadius = UDim.new(0, 2)

    local fillRatio = math.min(srv.playing / math.max(srv.maxPlayers, 1), 1)
    local BarFill = Instance.new("Frame", BarBG)
    BarFill.Size             = UDim2.new(fillRatio, 0, 1, 0)
    BarFill.BackgroundColor3 = fillRatio > 0.85
        and Color3.fromRGB(220, 60, 60) or Color3.fromRGB(80, 200, 120)
    BarFill.BorderSizePixel  = 0
    Instance.new("UICorner", BarFill).CornerRadius = UDim.new(0, 2)

    local pingStr   = srv.ping   and ("ð "..srv.ping.."ms ") or ""
    local label     = isCurrent  and " ð سيرفرك الحالي" or ""
    local regionStr = srv.region and (" ð "..srv.region) or ""
    local infoTxt = ('<b>%d / %d</b>%s%s%s\n<font color="#888899">%s</font>'):format(
        srv.playing, srv.maxPlayers, label, pingStr, regionStr,
        tostring(srv.id):sub(1,24)..'...'
    )

    local Info = Instance.new("TextLabel", Card)
    Info.Size               = UDim2.new(1, -130, 1, -12)
    Info.Position           = UDim2.new(0, 10, 0, 6)
    Info.BackgroundTransparency = 1
    Info.TextXAlignment     = Enum.TextXAlignment.Left
    Info.TextYAlignment     = Enum.TextYAlignment.Top
    Info.TextWrapped        = true
    Info.RichText           = true
    Info.TextSize           = 11
    Info.Font               = Enum.Font.Gotham
    Info.Text               = infoTxt
    Info.TextColor3         = isCurrent and Color3.fromRGB(120,255,120) or Color3.fromRGB(200,200,230)

    local JoinBtn = Instance.new("TextButton", Card)
    JoinBtn.Size             = UDim2.new(0, 100, 0, 32)
    JoinBtn.Position         = UDim2.new(1, -110, 0.5, -16)
    JoinBtn.BackgroundColor3 = isCurrent and Color3.fromRGB(50,50,50)
        or (isFull and Color3.fromRGB(80,30,30) or Color3.fromRGB(90,50,200))
    JoinBtn.TextColor3       = Color3.fromRGB(255, 255, 255)
    JoinBtn.Text             = isCurrent and "â أنت هنا" or (isFull and "ð´ ممتلئ" or "â¡ï¸ انضم")
    JoinBtn.Font             = Enum.Font.GothamBold
    JoinBtn.TextSize         = 12
    JoinBtn.BorderSizePixel  = 0
    JoinBtn.AutoButtonColor  = not isCurrent
    Instance.new("UICorner", JoinBtn).CornerRadius = UDim.new(0, 7)

    if not isCurrent and not isFull then
        JoinBtn.MouseButton1Click:Connect(function()
            spawnNotif("ð جاري الانتقال للسيرفر...", true)
            SafeTeleport(HUB_PLACE_ID, srv.id, LocalPlayer)
        end)
    end
end

local function HubRenderServers(list)
    HubClearCards()
    if hubStatusLabel then
        hubStatusLabel.Text = #list == 0
            and "â ï¸ لا توجد سيرفرات متاحة"
            or  ("â "..#list.." سيرفر — آخر تحديث: "..os.date("%H:%M:%S"))
    end
    for i, srv in ipairs(list) do
        HubMakeCard(srv, i)
    end
end

local function HubFetchServers()
    if hubIsFetching then return end
    hubIsFetching = true
    if hubStatusLabel then hubStatusLabel.Text = "â³ جاري جلب السيرفرات..." end
    HubClearCards()
    hubServerCache = {}

    task.spawn(function()
        local ok, result = pcall(function()
            local cursor    = ""
            local allSrvs   = {}
            for _ = 1, 10 do
                local url = ("https://games.roblox.com/v1/games/%d/servers/Public?sortOrder=Asc&limit=100"):format(HUB_PLACE_ID)
                if cursor ~= "" then url = url.."&cursor="..cursor end
                local raw  = game:HttpGetAsync(url)
                local data = HubHttpService:JSONDecode(raw)
                if data and data.data then
                    for _, s in ipairs(data.data) do
                        table.insert(allSrvs, {
                            id = s.id, playing = s.playing or 0,
                            maxPlayers = s.maxPlayers or 0, ping = s.ping, region = nil
                        })
                    end
                    cursor = data.nextPageCursor or ""
                    if cursor == "" then break end
                else break end
                task.wait(0.2)
            end
            table.sort(allSrvs, function(a,b) return a.playing < b.playing end)
            return allSrvs
        end)
        if ok then
            hubServerCache = result
            HubRenderServers(result)
        else
            if hubStatusLabel then hubStatusLabel.Text = "â فشل الجلب (HttpService معطّل؟)" end
        end
        hubIsFetching = false
    end)
end

local function InitHubUI()
    local HubTitle = Instance.new("TextLabel", PageHub)
    HubTitle.Size             = UDim2.new(0, 530, 0, 32)
    HubTitle.BackgroundColor3 = Color3.fromRGB(25, 25, 38)
    HubTitle.BorderSizePixel  = 0
    HubTitle.Text             = "ð Server Hub  —  Game: "..HUB_PLACE_ID
    HubTitle.TextColor3       = Color3.fromRGB(180, 140, 255)
    HubTitle.TextSize         = 14
    HubTitle.Font             = Enum.Font.GothamBold
    HubTitle.TextXAlignment   = Enum.TextXAlignment.Center
    Instance.new("UICorner", HubTitle).CornerRadius = UDim.new(0, 8)

    local ToolBar = Instance.new("Frame", PageHub)
    ToolBar.Size             = UDim2.new(0, 530, 0, 36)
    ToolBar.BackgroundColor3 = Color3.fromRGB(22, 22, 34)
    ToolBar.BorderSizePixel  = 0
    Instance.new("UICorner", ToolBar).CornerRadius = UDim.new(0, 8)
    local TBL = Instance.new("UIListLayout", ToolBar)
    TBL.FillDirection        = Enum.FillDirection.Horizontal
    TBL.Padding              = UDim.new(0, 6)
    TBL.VerticalAlignment    = Enum.VerticalAlignment.Center
    TBL.HorizontalAlignment  = Enum.HorizontalAlignment.Center

    local BtnRefresh    = MakeHubToolBtn(ToolBar, "ð تحديث",      110)
    local BtnJoinLeast  = MakeHubToolBtn(ToolBar, "ð أقل لاعبين", 130)
    local BtnJoinRandom = MakeHubToolBtn(ToolBar, "ð² عشوائي",     100)

    local SearchBox = Instance.new("TextBox", ToolBar)
    SearchBox.Size               = UDim2.new(0, 150, 0, 24)
    SearchBox.BackgroundColor3   = Color3.fromRGB(35, 35, 52)
    SearchBox.TextColor3         = Color3.fromRGB(220, 220, 255)
    SearchBox.PlaceholderText    = "ð ID السيرفر..."
    SearchBox.PlaceholderColor3  = Color3.fromRGB(100, 100, 140)
    SearchBox.Text               = ""
    SearchBox.Font               = Enum.Font.Gotham
    SearchBox.TextSize           = 11
    SearchBox.BorderSizePixel    = 0
    SearchBox.ClearTextOnFocus   = false
    Instance.new("UICorner", SearchBox).CornerRadius = UDim.new(0, 6)

    local CC = Instance.new("ScrollingFrame", PageHub)
    CC.Size                   = UDim2.new(0, 530, 0, 320)
    CC.BackgroundTransparency = 1
    CC.BorderSizePixel        = 0
    CC.ScrollBarThickness     = 3
    CC.ScrollBarImageColor3   = Color3.fromRGB(100, 60, 220)
    CC.CanvasSize             = UDim2.new(0,0,0,0)
    CC.ClipsDescendants       = true
    hubCardContainer = CC

    local CL = Instance.new("UIListLayout", CC)
    CL.Padding             = UDim.new(0, 5)
    CL.HorizontalAlignment = Enum.HorizontalAlignment.Center
    CL.SortOrder           = Enum.SortOrder.LayoutOrder
    local CP = Instance.new("UIPadding", CC)
    CP.PaddingTop    = UDim.new(0, 6)
    CP.PaddingBottom = UDim.new(0, 6)
    CL:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
        CC.CanvasSize = UDim2.new(0, 0, 0, CL.AbsoluteContentSize.Y + 20)
    end)

    local SL = Instance.new("TextLabel", PageHub)
    SL.Size                  = UDim2.new(0, 530, 0, 24)
    SL.BackgroundTransparency = 1
    SL.Text                  = "ð اضغط تحديث لجلب السيرفرات"
    SL.TextColor3            = Color3.fromRGB(140, 140, 180)
    SL.TextSize              = 12
    SL.Font                  = Enum.Font.Gotham
    SL.TextXAlignment        = Enum.TextXAlignment.Center
    hubStatusLabel = SL

    BtnRefresh.MouseButton1Click:Connect(HubFetchServers)

    BtnJoinLeast.MouseButton1Click:Connect(function()
        if #hubServerCache == 0 then spawnNotif("â ï¸ حدّث القائمة أولاً", false) return end
        local best = nil
        for _, s in ipairs(hubServerCache) do
            if s.id ~= game.JobId and s.playing < s.maxPlayers then
                if not best or s.playing < best.playing then best = s end
            end
        end
        if best then
            spawnNotif("ð انضمام لأقل سيرفر ازدحامًا...", true)
            SafeTeleport(HUB_PLACE_ID, best.id, LocalPlayer)
        else
            spawnNotif("â ï¸ لا يوجد سيرفر متاح", false)
        end
    end)

    BtnJoinRandom.MouseButton1Click:Connect(function()
        if #hubServerCache == 0 then spawnNotif("â ï¸ حدّث القائمة أولاً", false) return end
        local cands = {}
        for _, s in ipairs(hubServerCache) do
            if s.id ~= game.JobId and s.playing < s.maxPlayers then
                table.insert(cands, s)
            end
        end
        if #cands > 0 then
            local pick = cands[math.random(1, #cands)]
            spawnNotif("ð² انضمام لسيرفر عشوائي...", true)
            SafeTeleport(HUB_PLACE_ID, pick.id, LocalPlayer)
        else
            spawnNotif("â ï¸ لا يوجد سيرفر متاح", false)
        end
    end)

    SearchBox:GetPropertyChangedSignal("Text"):Connect(function()
        local q = SearchBox.Text:lower()
        if q == "" then
            HubRenderServers(hubServerCache)
        else
            local filtered = {}
            for _, s in ipairs(hubServerCache) do
                if tostring(s.id):lower():find(q, 1, true) then
                    table.insert(filtered, s)
                end
            end
            HubRenderServers(filtered)
        end
    end)
end

InitHubUI()

print("✅ Elite Ace GUI + Scanner تم التحميل | RightShift للإخفاء | تاب 🔍 Scanner للسكانر | تاب 🌐 Hub للسيرفرات")
