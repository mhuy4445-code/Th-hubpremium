-- ==========================================
-- THỌ HUB - MULTI-GAME LOADER (UPDATED)
-- ==========================================

local CoreGui = game:GetService("CoreGui")
local Players = game:GetService("Players")
local TeleportService = game:GetService("TeleportService")
local LocalPlayer = Players.LocalPlayer

if CoreGui:FindFirstChild("ThoHubLoaderUI") then
    CoreGui.ThoHubLoaderUI:Destroy()
end

-- 1. Khởi tạo Giao diện (ScreenGui)
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "ThoHubLoaderUI"
ScreenGui.Parent = CoreGui
ScreenGui.ResetOnSpawn = false

-- 2. Khung chứa chính (MainFrame)
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 440, 0, 420)
MainFrame.Position = UDim2.new(0.5, -220, 0.5, -210)
MainFrame.BackgroundColor3 = Color3.fromRGB(12, 16, 24)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.ClipsDescendants = true
MainFrame.Parent = ScreenGui

local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 12)
UICorner.Parent = MainFrame

-- Viền phát sáng nhẹ tạo điểm nhấn cao cấp
local UIStroke = Instance.new("UIStroke")
UIStroke.Color = Color3.fromRGB(35, 70, 110)
UIStroke.Thickness = 1.5
UIStroke.Parent = MainFrame

-- Thanh tiêu đề (Header Bar) tích hợp Gradient
local Header = Instance.new("Frame")
Header.Name = "Header"
Header.Size = UDim2.new(1, 0, 0, 48)
Header.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Header.BorderSizePixel = 0
Header.Parent = MainFrame

local HeaderGradient = Instance.new("UIGradient")
HeaderGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(20, 45, 80)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(15, 30, 55))
})
HeaderGradient.Parent = Header

local HeaderCorner = Instance.new("UICorner")
HeaderCorner.CornerRadius = UDim.new(0, 12)
HeaderCorner.Parent = Header

local HeaderCover = Instance.new("Frame")
HeaderCover.Size = UDim2.new(1, 0, 0, 10)
HeaderCover.Position = UDim2.new(0, 0, 1, -10)
HeaderCover.BackgroundColor3 = Color3.fromRGB(20, 45, 80)
HeaderCover.BorderSizePixel = 0
HeaderCover.Parent = Header

local LogoIcon = Instance.new("ImageLabel")
LogoIcon.Name = "LogoIcon"
LogoIcon.Size = UDim2.new(0, 32, 0, 32)
LogoIcon.Position = UDim2.new(0.5, -16, 0.5, -16)
LogoIcon.BackgroundTransparency = 1
LogoIcon.Image = "rbxassetid://112185134254493" 
LogoIcon.Visible = false
LogoIcon.Parent = Header

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, -90, 1, 0)
Title.Position = UDim2.new(0, 16, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "⚡ THỌ HUB - LOADER"
Title.TextColor3 = Color3.fromRGB(130, 220, 255)
Title.TextSize = 15
Title.Font = Enum.Font.GothamBold
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Parent = Header

-- Nút Thu nhỏ (-)
local MinimizeBtn = Instance.new("TextButton")
MinimizeBtn.Size = UDim2.new(0, 30, 0, 30)
MinimizeBtn.Position = UDim2.new(1, -74, 0.5, -15)
MinimizeBtn.BackgroundColor3 = Color3.fromRGB(30, 60, 95)
MinimizeBtn.Text = "-"
MinimizeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeBtn.Font = Enum.Font.GothamBold
MinimizeBtn.TextSize = 18
MinimizeBtn.Parent = Header

local MinCorner = Instance.new("UICorner")
MinCorner.CornerRadius = UDim.new(0, 8)
MinCorner.Parent = MinimizeBtn

-- Nút Đóng (X)
local CloseBtn = Instance.new("TextButton")
CloseBtn.Size = UDim2.new(0, 30, 0, 30)
CloseBtn.Position = UDim2.new(1, -38, 0.5, -15)
CloseBtn.BackgroundColor3 = Color3.fromRGB(220, 60, 60)
CloseBtn.Text = "×"
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.Font = Enum.Font.GothamBold
CloseBtn.TextSize = 20
CloseBtn.Parent = Header

local CloseCorner = Instance.new("UICorner")
CloseCorner.CornerRadius = UDim.new(0, 8)
CloseCorner.Parent = CloseBtn

-- Forward declarations cho containers
local BloxFruitContainer, StealEggContainer, SupportContainer, TabBar

-- Xử lý nút Thu nhỏ (-)
local isMinimized = false
MinimizeBtn.MouseButton1Click:Connect(function()
    isMinimized = not isMinimized
    BloxFruitContainer.Visible = not isMinimized and TabBar.Visible
    StealEggContainer.Visible = false
    SupportContainer.Visible = false
    TabBar.Visible = not isMinimized
    LogoIcon.Visible = isMinimized
    Title.Visible = not isMinimized
    MainFrame.Size = isMinimized and UDim2.new(0, 440, 0, 48) or UDim2.new(0, 440, 0, 420)
    MinimizeBtn.Text = isMinimized and "+" or "-"
end)

-- Xử lý nút Đóng (×)
CloseBtn.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- 3. Thanh Chuyển Tab (Tab Bar - Gồm 3 Tab)
TabBar = Instance.new("Frame")
TabBar.Name = "TabBar"
TabBar.Size = UDim2.new(1, -24, 0, 36)
TabBar.Position = UDim2.new(0, 12, 0, 56)
TabBar.BackgroundTransparency = 1
TabBar.Parent = MainFrame

local TabBloxFruitBtn = Instance.new("TextButton")
TabBloxFruitBtn.Name = "TabBloxFruitBtn"
TabBloxFruitBtn.Size = UDim2.new(0.33, -4, 1, 0)
TabBloxFruitBtn.BackgroundColor3 = Color3.fromRGB(0, 140, 255)
TabBloxFruitBtn.Text = "🍎 Blox Fruit"
TabBloxFruitBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
TabBloxFruitBtn.Font = Enum.Font.GothamBold
TabBloxFruitBtn.TextSize = 12
TabBloxFruitBtn.Parent = TabBar

local Tab1Corner = Instance.new("UICorner")
Tab1Corner.CornerRadius = UDim.new(0, 8)
Tab1Corner.Parent = TabBloxFruitBtn

local TabStealEggBtn = Instance.new("TextButton")
TabStealEggBtn.Name = "TabStealEggBtn"
TabStealEggBtn.Size = UDim2.new(0.33, -4, 1, 0)
TabStealEggBtn.Position = UDim2.new(0.33, 2, 0, 0)
TabStealEggBtn.BackgroundColor3 = Color3.fromRGB(22, 30, 45)
TabStealEggBtn.Text = "🥚 Steal An Egg"
TabStealEggBtn.TextColor3 = Color3.fromRGB(160, 180, 205)
TabStealEggBtn.Font = Enum.Font.GothamBold
TabStealEggBtn.TextSize = 11
TabStealEggBtn.Parent = TabBar

local Tab3Corner = Instance.new("UICorner")
Tab3Corner.CornerRadius = UDim.new(0, 8)
Tab3Corner.Parent = TabStealEggBtn

local TabSupportBtn = Instance.new("TextButton")
TabSupportBtn.Name = "TabSupportBtn"
TabSupportBtn.Size = UDim2.new(0.33, -4, 1, 0)
TabSupportBtn.Position = UDim2.new(0.66, 4, 0, 0)
TabSupportBtn.BackgroundColor3 = Color3.fromRGB(22, 30, 45)
TabSupportBtn.Text = "🛠️ Hỗ trợ"
TabSupportBtn.TextColor3 = Color3.fromRGB(160, 180, 205)
TabSupportBtn.Font = Enum.Font.GothamBold
TabSupportBtn.TextSize = 12
TabSupportBtn.Parent = TabBar

local Tab2Corner = Instance.new("UICorner")
Tab2Corner.CornerRadius = UDim.new(0, 8)
Tab2Corner.Parent = TabSupportBtn

-- Containers
BloxFruitContainer = Instance.new("ScrollingFrame")
BloxFruitContainer.Name = "BloxFruitContainer"
BloxFruitContainer.Size = UDim2.new(1, -24, 1, -106)
BloxFruitContainer.Position = UDim2.new(0, 12, 0, 100)
BloxFruitContainer.BackgroundTransparency = 1
BloxFruitContainer.BorderSizePixel = 0
BloxFruitContainer.ScrollBarThickness = 4
BloxFruitContainer.ScrollBarImageColor3 = Color3.fromRGB(0, 140, 255)
BloxFruitContainer.Parent = MainFrame

local BloxFruitListLayout = Instance.new("UIListLayout")
BloxFruitListLayout.Parent = BloxFruitContainer
BloxFruitListLayout.SortOrder = Enum.SortOrder.LayoutOrder
BloxFruitListLayout.Padding = UDim.new(0, 8)
BloxFruitListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    BloxFruitContainer.CanvasSize = UDim2.new(0, 0, 0, BloxFruitListLayout.AbsoluteContentSize.Y + 12)
end)

StealEggContainer = Instance.new("ScrollingFrame")
StealEggContainer.Name = "StealEggContainer"
StealEggContainer.Size = UDim2.new(1, -24, 1, -106)
StealEggContainer.Position = UDim2.new(0, 12, 0, 100)
StealEggContainer.BackgroundTransparency = 1
StealEggContainer.BorderSizePixel = 0
StealEggContainer.Visible = false
StealEggContainer.ScrollBarThickness = 4
StealEggContainer.ScrollBarImageColor3 = Color3.fromRGB(0, 140, 255)
StealEggContainer.Parent = MainFrame

local StealEggListLayout = Instance.new("UIListLayout")
StealEggListLayout.Parent = StealEggContainer
StealEggListLayout.SortOrder = Enum.SortOrder.LayoutOrder
StealEggListLayout.Padding = UDim.new(0, 8)
StealEggListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    StealEggContainer.CanvasSize = UDim2.new(0, 0, 0, StealEggListLayout.AbsoluteContentSize.Y + 12)
end)

SupportContainer = Instance.new("ScrollingFrame")
SupportContainer.Name = "SupportContainer"
SupportContainer.Size = UDim2.new(1, -24, 1, -106)
SupportContainer.Position = UDim2.new(0, 12, 0, 100)
SupportContainer.BackgroundTransparency = 1
SupportContainer.BorderSizePixel = 0
SupportContainer.Visible = false
SupportContainer.ScrollBarThickness = 4
SupportContainer.ScrollBarImageColor3 = Color3.fromRGB(0, 140, 255)
SupportContainer.Parent = MainFrame

local SupportListLayout = Instance.new("UIListLayout")
SupportListLayout.Parent = SupportContainer
SupportListLayout.SortOrder = Enum.SortOrder.LayoutOrder
SupportListLayout.Padding = UDim.new(0, 8)
SupportListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    SupportContainer.CanvasSize = UDim2.new(0, 0, 0, SupportListLayout.AbsoluteContentSize.Y + 12)
end)

-- Sự kiện bấm chuyển Tab
TabBloxFruitBtn.MouseButton1Click:Connect(function()
    BloxFruitContainer.Visible = true
    StealEggContainer.Visible = false
    SupportContainer.Visible = false
    TabBloxFruitBtn.BackgroundColor3 = Color3.fromRGB(0, 140, 255)
    TabBloxFruitBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    TabStealEggBtn.BackgroundColor3 = Color3.fromRGB(22, 30, 45)
    TabStealEggBtn.TextColor3 = Color3.fromRGB(160, 180, 205)
    TabSupportBtn.BackgroundColor3 = Color3.fromRGB(22, 30, 45)
    TabSupportBtn.TextColor3 = Color3.fromRGB(160, 180, 205)
end)

TabStealEggBtn.MouseButton1Click:Connect(function()
    BloxFruitContainer.Visible = false
    StealEggContainer.Visible = true
    SupportContainer.Visible = false
    TabBloxFruitBtn.BackgroundColor3 = Color3.fromRGB(22, 30, 45)
    TabBloxFruitBtn.TextColor3 = Color3.fromRGB(160, 180, 205)
    TabStealEggBtn.BackgroundColor3 = Color3.fromRGB(0, 140, 255)
    TabStealEggBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    TabSupportBtn.BackgroundColor3 = Color3.fromRGB(22, 30, 45)
    TabSupportBtn.TextColor3 = Color3.fromRGB(160, 180, 205)
end)

TabSupportBtn.MouseButton1Click:Connect(function()
    BloxFruitContainer.Visible = false
    StealEggContainer.Visible = false
    SupportContainer.Visible = true
    TabBloxFruitBtn.BackgroundColor3 = Color3.fromRGB(22, 30, 45)
    TabBloxFruitBtn.TextColor3 = Color3.fromRGB(160, 180, 205)
    TabStealEggBtn.BackgroundColor3 = Color3.fromRGB(22, 30, 45)
    TabStealEggBtn.TextColor3 = Color3.fromRGB(160, 180, 205)
    TabSupportBtn.BackgroundColor3 = Color3.fromRGB(0, 140, 255)
    TabSupportBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
end)

-- 4. Danh sách Blox Fruit Scripts
local hubList = {
    { Name = "DatThg V2", URL = "https://raw.githubusercontent.com/LuaCrack/DatThg/refs/heads/main/DatThgV2" },
    { Name = "Red Hub", URL = "https://raw.githubusercontent.com/realredz/BloxFruits/refs/heads/main/Source.lua" },
    { Name = "Hoho Hub", URL = "https://raw.githubusercontent.com/acsu123/HOHO_H/main/Loading_UI" },
    { Name = "Realkid Hub", URL = "https://raw.githubusercontent.com/realkidhub/realkid/refs/heads/main/main.lua" },
    { Name = "Gravity Hub", URL = "https://raw.githubusercontent.com/Dev-GravityHub/BloxFruit/refs/heads/main/Main.lua" },
    { Name = "Trẩu Hub", URL = "https://raw.githubusercontent.com/trungdao2k4/buffalo/refs/heads/main/trauhubv10" },
    { 
        Name = "Nhặt Rương", 
        CustomRun = function()
            repeat task.wait() until game:IsLoaded() and LocalPlayer
            getgenv().Team = "Marines"
            loadstring(game:HttpGet("https://raw.githubusercontent.com/trongdeptraihucscript/Main/refs/heads/main/TN-Tp-Chest.lua"))()
        end
    },
    { Name = "Night Hub", URL = "https://github.com/WhiteX1208/Scripts/blob/main/HopScript.luau?raw=true" }
}

for _, hub in ipairs(hubList) do
    local ItemFrame = Instance.new("Frame")
    ItemFrame.Size = UDim2.new(1, -6, 0, 38)
    ItemFrame.BackgroundColor3 = Color3.fromRGB(18, 24, 36)
    ItemFrame.Parent = BloxFruitContainer

    local ItemCorner = Instance.new("UICorner")
    ItemCorner.CornerRadius = UDim.new(0, 8)
    ItemCorner.Parent = ItemFrame

    local ItemStroke = Instance.new("UIStroke")
    ItemStroke.Color = Color3.fromRGB(30, 42, 64)
    ItemStroke.Thickness = 1
    ItemStroke.Parent = ItemFrame

    local HubLabel = Instance.new("TextLabel")
    HubLabel.Size = UDim2.new(1, -110, 1, 0)
    HubLabel.Position = UDim2.new(0, 14, 0, 0)
    HubLabel.BackgroundTransparency = 1
    HubLabel.Text = hub.Name
    HubLabel.TextColor3 = Color3.fromRGB(230, 240, 255)
    HubLabel.Font = Enum.Font.GothamMedium
    HubLabel.TextSize = 13.5
    HubLabel.TextXAlignment = Enum.TextXAlignment.Left
    HubLabel.Parent = ItemFrame

    local ExecBtn = Instance.new("TextButton")
    ExecBtn.Size = UDim2.new(0, 92, 0, 26)
    ExecBtn.Position = UDim2.new(1, -98, 0.5, -13)
    ExecBtn.BackgroundColor3 = Color3.fromRGB(0, 130, 235)
    ExecBtn.Text = "Execute"
    ExecBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    ExecBtn.Font = Enum.Font.GothamBold
    ExecBtn.TextSize = 12
    ExecBtn.Parent = ItemFrame

    local ExecCorner = Instance.new("UICorner")
    ExecCorner.CornerRadius = UDim.new(0, 6)
    ExecCorner.Parent = ExecBtn

    ExecBtn.MouseButton1Click:Connect(function()
        ExecBtn.Text = "Loading..."
        ExecBtn.BackgroundColor3 = Color3.fromRGB(200, 140, 0)

        local success, err = pcall(function()
            if hub.CustomRun then
                hub.CustomRun()
            else
                loadstring(game:HttpGet(hub.URL))()
            end
        end)

        if success then
            ExecBtn.Text = "Success!"
            ExecBtn.BackgroundColor3 = Color3.fromRGB(0, 185, 110)
        else
            ExecBtn.Text = "Error!"
            ExecBtn.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
            warn("[Thọ Hub Error - " .. hub.Name .. "]: " .. tostring(err))
        end

        task.wait(2)
        ExecBtn.Text = "Execute"
        ExecBtn.BackgroundColor3 = Color3.fromRGB(0, 130, 235)
    end)
end

-- 5. Danh sách Steal An Egg Scripts (Tab mới)
local stealEggList = {
    { Name = "Ouroboros Hub", URL = "https://raw.githubusercontent.com/joustingmatch/Ouroboros/main/loader.lua" },
    { Name = "Night Hub", URL = "https://raw.githubusercontent.com/WhiteX1208/Scripts/refs/heads/main/StealAnEggs.luau" },
    { Name = "Fox Name Hub", URL = "https://raw.githubusercontent.com/caomod2077/Script/refs/heads/main/Fn-stealanegg.lua" },
    { 
        Name = "Decode Hub", 
        CustomRun = function()
            loadstring(game:HttpGet("https://raw.githubusercontent.com/ItzYumi/Decode/refs/heads/main/DE%3ACODE.lua", true))()
        end
    }
}

for _, item in ipairs(stealEggList) do
    local ItemFrame = Instance.new("Frame")
    ItemFrame.Size = UDim2.new(1, -6, 0, 38)
    ItemFrame.BackgroundColor3 = Color3.fromRGB(18, 24, 36)
    ItemFrame.Parent = StealEggContainer

    local ItemCorner = Instance.new("UICorner")
    ItemCorner.CornerRadius = UDim.new(0, 8)
    ItemCorner.Parent = ItemFrame

    local ItemStroke = Instance.new("UIStroke")
    ItemStroke.Color = Color3.fromRGB(30, 42, 64)
    ItemStroke.Thickness = 1
    ItemStroke.Parent = ItemFrame

    local Label = Instance.new("TextLabel")
    Label.Size = UDim2.new(1, -110, 1, 0)
    Label.Position = UDim2.new(0, 14, 0, 0)
    Label.BackgroundTransparency = 1
    Label.Text = item.Name
    Label.TextColor3 = Color3.fromRGB(230, 240, 255)
    Label.Font = Enum.Font.GothamMedium
    Label.TextSize = 13.5
    Label.TextXAlignment = Enum.TextXAlignment.Left
    Label.Parent = ItemFrame

    local ExecBtn = Instance.new("TextButton")
    ExecBtn.Size = UDim2.new(0, 92, 0, 26)
    ExecBtn.Position = UDim2.new(1, -98, 0.5, -13)
    ExecBtn.BackgroundColor3 = Color3.fromRGB(0, 130, 235)
    ExecBtn.Text = "Execute"
    ExecBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    ExecBtn.Font = Enum.Font.GothamBold
    ExecBtn.TextSize = 12
    ExecBtn.Parent = ItemFrame

    local ExecCorner = Instance.new("UICorner")
    ExecCorner.CornerRadius = UDim.new(0, 6)
    ExecCorner.Parent = ExecBtn

    ExecBtn.MouseButton1Click:Connect(function()
        ExecBtn.Text = "Loading..."
        ExecBtn.BackgroundColor3 = Color3.fromRGB(200, 140, 0)

        local success, err = pcall(function()
            if item.CustomRun then
                item.CustomRun()
            else
                loadstring(game:HttpGet(item.URL))()
            end
        end)

        if success then
            ExecBtn.Text = "Success!"
            ExecBtn.BackgroundColor3 = Color3.fromRGB(0, 185, 110)
        else
            ExecBtn.Text = "Error!"
            ExecBtn.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
            warn("[Thọ Hub Error - " .. item.Name .. "]: " .. tostring(err))
        end

        task.wait(2)
        ExecBtn.Text = "Execute"
        ExecBtn.BackgroundColor3 = Color3.fromRGB(0, 130, 235)
    end)
end

-- 6. Danh sách Hỗ trợ
local supportList = {
    {
        Name = "Fly GUI V3",
        Func = function()
            loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Fly-gui-v3-30439"))()
        end
    },
    {
        Name = "Vào lại Server (Rejoin)",
        Func = function()
            TeleportService:Teleport(game.PlaceId, LocalPlayer)
        end
    }
}

for _, item in ipairs(supportList) do
    local ItemFrame = Instance.new("Frame")
    ItemFrame.Size = UDim2.new(1, -6, 0, 38)
    ItemFrame.BackgroundColor3 = Color3.fromRGB(18, 24, 36)
    ItemFrame.Parent = SupportContainer

    local ItemCorner = Instance.new("UICorner")
    ItemCorner.CornerRadius = UDim.new(0, 8)
    ItemCorner.Parent = ItemFrame

    local ItemStroke = Instance.new("UIStroke")
    ItemStroke.Color = Color3.fromRGB(30, 42, 64)
    ItemStroke.Thickness = 1
    ItemStroke.Parent = ItemFrame

    local Label = Instance.new("TextLabel")
    Label.Size = UDim2.new(1, -110, 1, 0)
    Label.Position = UDim2.new(0, 14, 0, 0)
    Label.BackgroundTransparency = 1
    Label.Text = item.Name
    Label.TextColor3 = Color3.fromRGB(230, 240, 255)
    Label.Font = Enum.Font.GothamMedium
    Label.TextSize = 13.5
    Label.TextXAlignment = Enum.TextXAlignment.Left
    Label.Parent = ItemFrame

    local ExecBtn = Instance.new("TextButton")
    ExecBtn.Size = UDim2.new(0, 92, 0, 26)
    ExecBtn.Position = UDim2.new(1, -98, 0.5, -13)
    ExecBtn.BackgroundColor3 = Color3.fromRGB(0, 130, 235)
    ExecBtn.Text = "Execute"
    ExecBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    ExecBtn.Font = Enum.Font.GothamBold
    ExecBtn.TextSize = 12
    ExecBtn.Parent = ItemFrame

    local ExecCorner = Instance.new("UICorner")
    ExecCorner.CornerRadius = UDim.new(0, 6)
    ExecCorner.Parent = ExecBtn

    ExecBtn.MouseButton1Click:Connect(function()
        ExecBtn.Text = "Loading..."
        ExecBtn.BackgroundColor3 = Color3.fromRGB(200, 140, 0)

        local success, err = pcall(function()
            if item.Func then
                item.Func()
            end
        end)

        if success then
            ExecBtn.Text = "Success!"
            ExecBtn.BackgroundColor3 = Color3.fromRGB(0, 185, 110)
        else
            ExecBtn.Text = "Error!"
            ExecBtn.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
            warn("[Thọ Hub Error - " .. item.Name .. "]: " .. tostring(err))
        end

        task.wait(2)
        ExecBtn.Text = "Execute"
        ExecBtn.BackgroundColor3 = Color3.fromRGB(0, 130, 235)
    end)
end

