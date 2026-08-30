-- 1. Khởi tạo Giao diện (ScreenGui)
local CoreGui = game:GetService("CoreGui")

if CoreGui:FindFirstChild("ThoHubLoaderUI") then
    CoreGui.ThoHubLoaderUI:Destroy()
end

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "ThoHubLoaderUI"
ScreenGui.Parent = CoreGui
ScreenGui.ResetOnSpawn = false

-- 2. Khung chứa chính (MainFrame)
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 420, 0, 400)
MainFrame.Position = UDim2.new(0.5, -210, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 20, 30)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.ClipsDescendants = true
MainFrame.Parent = ScreenGui

local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 10)
UICorner.Parent = MainFrame

-- Thanh tiêu đề (Header Bar)
local Header = Instance.new("Frame")
Header.Name = "Header"
Header.Size = UDim2.new(1, 0, 0, 45)
Header.BackgroundColor3 = Color3.fromRGB(20, 40, 65)
Header.BorderSizePixel = 0
Header.Parent = MainFrame

local HeaderCorner = Instance.new("UICorner")
HeaderCorner.CornerRadius = UDim.new(0, 10)
HeaderCorner.Parent = Header

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, -80, 1, 0)
Title.Position = UDim2.new(0, 15, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "Thọ Hub"
Title.TextColor3 = Color3.fromRGB(140, 210, 255)
Title.TextSize = 18
Title.Font = Enum.Font.SourceSansBold
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Parent = Header

-- Nút Thu nhỏ (-)
local MinimizeBtn = Instance.new("TextButton")
MinimizeBtn.Size = UDim2.new(0, 28, 0, 28)
MinimizeBtn.Position = UDim2.new(1, -68, 0.5, -14)
MinimizeBtn.BackgroundColor3 = Color3.fromRGB(30, 60, 95)
MinimizeBtn.Text = "-"
MinimizeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeBtn.Font = Enum.Font.SourceSansBold
MinimizeBtn.TextSize = 20
MinimizeBtn.Parent = Header

local MinCorner = Instance.new("UICorner")
MinCorner.CornerRadius = UDim.new(0, 6)
MinCorner.Parent = MinimizeBtn

-- Nút Đóng (X)
local CloseBtn = Instance.new("TextButton")
CloseBtn.Size = UDim2.new(0, 28, 0, 28)
CloseBtn.Position = UDim2.new(1, -34, 0.5, -14)
CloseBtn.BackgroundColor3 = Color3.fromRGB(210, 50, 50)
CloseBtn.Text = "X"
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.Font = Enum.Font.SourceSansBold
CloseBtn.TextSize = 14
CloseBtn.Parent = Header

local CloseCorner = Instance.new("UICorner")
CloseCorner.CornerRadius = UDim.new(0, 6)
CloseCorner.Parent = CloseBtn

-- 3. Thanh Chuyển Tab (Tab Bar)
local TabBar = Instance.new("Frame")
TabBar.Name = "TabBar"
TabBar.Size = UDim2.new(1, -20, 0, 32)
TabBar.Position = UDim2.new(0, 10, 0, 50)
TabBar.BackgroundTransparency = 1
TabBar.Parent = MainFrame

local TabScriptBtn = Instance.new("TextButton")
TabScriptBtn.Name = "TabScriptBtn"
TabScriptBtn.Size = UDim2.new(0.5, -4, 1, 0)
TabScriptBtn.BackgroundColor3 = Color3.fromRGB(0, 130, 220)
TabScriptBtn.Text = "Script"
TabScriptBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
TabScriptBtn.Font = Enum.Font.SourceSansBold
TabScriptBtn.TextSize = 14
TabScriptBtn.Parent = TabBar

local Tab1Corner = Instance.new("UICorner")
Tab1Corner.CornerRadius = UDim.new(0, 6)
Tab1Corner.Parent = TabScriptBtn

local TabSupportBtn = Instance.new("TextButton")
TabSupportBtn.Name = "TabSupportBtn"
TabSupportBtn.Size = UDim2.new(0.5, -4, 1, 0)
TabSupportBtn.Position = UDim2.new(0.5, 4, 0, 0)
TabSupportBtn.BackgroundColor3 = Color3.fromRGB(25, 35, 50)
TabSupportBtn.Text = "Hỗ trợ"
TabSupportBtn.TextColor3 = Color3.fromRGB(180, 200, 220)
TabSupportBtn.Font = Enum.Font.SourceSansBold
TabSupportBtn.TextSize = 14
TabSupportBtn.Parent = TabBar

local Tab2Corner = Instance.new("UICorner")
Tab2Corner.CornerRadius = UDim.new(0, 6)
Tab2Corner.Parent = TabSupportBtn

-- === MỤC 1: TAB SCRIPT ===
local ScriptContainer = Instance.new("ScrollingFrame")
ScriptContainer.Name = "ScriptContainer"
ScriptContainer.Size = UDim2.new(1, -20, 1, -95)
ScriptContainer.Position = UDim2.new(0, 10, 0, 90)
ScriptContainer.BackgroundTransparency = 1
ScriptContainer.BorderSizePixel = 0
ScriptContainer.ScrollBarThickness = 5
ScriptContainer.ScrollBarImageColor3 = Color3.fromRGB(0, 120, 215)
ScriptContainer.Parent = MainFrame

local ScriptListLayout = Instance.new("UIListLayout")
ScriptListLayout.Parent = ScriptContainer
ScriptListLayout.SortOrder = Enum.SortOrder.LayoutOrder
ScriptListLayout.Padding = UDim.new(0, 8)

ScriptListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    ScriptContainer.CanvasSize = UDim2.new(0, 0, 0, ScriptListLayout.AbsoluteContentSize.Y + 10)
end)

-- === MỤC 2: TAB HỖ TRỢ ===
local SupportContainer = Instance.new("ScrollingFrame")
SupportContainer.Name = "SupportContainer"
SupportContainer.Size = UDim2.new(1, -20, 1, -95)
SupportContainer.Position = UDim2.new(0, 10, 0, 90)
SupportContainer.BackgroundTransparency = 1
SupportContainer.BorderSizePixel = 0
SupportContainer.Visible = false
SupportContainer.ScrollBarThickness = 5
SupportContainer.ScrollBarImageColor3 = Color3.fromRGB(0, 120, 215)
SupportContainer.Parent = MainFrame

local SupportListLayout = Instance.new("UIListLayout")
SupportListLayout.Parent = SupportContainer
SupportListLayout.SortOrder = Enum.SortOrder.LayoutOrder
SupportListLayout.Padding = UDim.new(0, 8)

SupportListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    SupportContainer.CanvasSize = UDim2.new(0, 0, 0, SupportListLayout.AbsoluteContentSize.Y + 10)
end)

-- 4. Danh sách Hubs trong mục Script
local hubList = {
    { Name = "Quantum Onyx", URL = "https://raw.githubusercontent.com/flazhy/QuantumOnyx/refs/heads/main/QuantumOnyx.lua" },
    { Name = "Pole Hub", URL = "https://raw.githubusercontent.com/Banana/refs/heads/main/Pole/script.luau" },
    { Name = "Comet Hub", URL = "https://raw.githubusercontent.com/Stellar/refs/heads/main/Comet/script.luau" },
    { Name = "EZ Hub", URL = "https://raw.githubusercontent.com/Fluent/refs/heads/main/EZ/script.luau" },
    { Name = "GB Hub", URL = "https://raw.githubusercontent.com/Banana/refs/heads/main/GB/script.luau" },
    { Name = "DB Hub", URL = "https://raw.githubusercontent.com/Banana/refs/heads/main/DB/script.luau" },
    { Name = "Wind Hub", URL = "https://raw.githubusercontent.com/Wind/refs/heads/main/Wind/script.luau" },
    { Name = "Star Hub", URL = "https://raw.githubusercontent.com/Stellar/refs/heads/main/Star/script.luau" },
    { Name = "ARC Hub", URL = "https://raw.githubusercontent.com/Arclylic/refs/heads/main/ARC/script.luau" },
    { Name = "Brave Hub", URL = "https://raw.githubusercontent.com/FruitBlox/refs/heads/main/BraveLoader", HasFlag = true },
    { Name = "Longhihi Hub", URL = "https://raw.githubusercontent.com/LongHiHiV4.5.1/refs/heads/main/Main.Txt.Luau" },
    { Name = "Ndraawz Hub", URL = "https://api-ndraawz.vercel.app/api/v1/NZ-DAE0SFRD00" },
    { Name = "Relz Hub", URL = "https://relzhub.com/loader" },
    { Name = "Vezyra Hub", URL = "https://raw.githubusercontent.com/Vezyra/refs/heads/main/VezyraHubMainBloxFruit.lua.txt" },
    { Name = "FE Vehicle Script V2", URL = "https://rawscripts.net/raw/Universal-Script-FE-Vehicle-Script-V2-88610" },
    { Name = "Client Replication - John Doe", URL = "https://rawscripts.net/raw/Client-Replication-John-doe-up-by-gojohdkaisenkt-34198" },
    { Name = "Tiger X", URL = "https://rawscripts.net/raw/Universal-Script-Tiger-x-34229" }
}

for _, hub in ipairs(hubList) do
    local ItemFrame = Instance.new("Frame")
    ItemFrame.Size = UDim2.new(1, -10, 0, 36)
    ItemFrame.BackgroundColor3 = Color3.fromRGB(22, 30, 45)
    ItemFrame.Parent = ScriptContainer

    local ItemCorner = Instance.new("UICorner")
    ItemCorner.CornerRadius = UDim.new(0, 6)
    ItemCorner.Parent = ItemFrame

    local HubLabel = Instance.new("TextLabel")
    HubLabel.Size = UDim2.new(1, -110, 1, 0)
    HubLabel.Position = UDim2.new(0, 12, 0, 0)
    HubLabel.BackgroundTransparency = 1
    HubLabel.Text = hub.Name
    HubLabel.TextColor3 = Color3.fromRGB(220, 235, 255)
    HubLabel.Font = Enum.Font.SourceSansSemibold
    HubLabel.TextSize = 15
    HubLabel.TextXAlignment = Enum.TextXAlignment.Left
    HubLabel.Parent = ItemFrame

    local ExecBtn = Instance.new("TextButton")
    ExecBtn.Size = UDim2.new(0, 90, 0, 26)
    ExecBtn.Position = UDim2.new(1, -96, 0.5, -13)
    ExecBtn.BackgroundColor3 = Color3.fromRGB(0, 130, 220)
    ExecBtn.Text = "Execute"
    ExecBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    ExecBtn.Font = Enum.Font.SourceSansBold
    ExecBtn.TextSize = 13
    ExecBtn.Parent = ItemFrame

    local ExecCorner = Instance.new("UICorner")
    ExecCorner.CornerRadius = UDim.new(0, 5)
    ExecCorner.Parent = ExecBtn

    ExecBtn.MouseButton1Click:Connect(function()
        ExecBtn.Text = "Loading..."
        ExecBtn.BackgroundColor3 = Color3.fromRGB(180, 130, 0)

        local success, err = pcall(function()
            if hub.HasFlag then
                loadstring(game:HttpGet(hub.URL, true))()
            else
                loadstring(game:HttpGet(hub.URL))()
            end
        end)

        if success then
            ExecBtn.Text = "Success!"
            ExecBtn.BackgroundColor3 = Color3.fromRGB(0, 180, 120)
        else
            ExecBtn.Text = "Error!"
            ExecBtn.BackgroundColor3 = Color3.fromRGB(180, 40, 40)
            warn("[Thọ Hub Error - " .. hub.Name .. "]: " .. tostring(err))
        end

        task.wait(2)
        ExecBtn.Text = "Execute"
        ExecBtn.BackgroundColor3 = Color3.fromRGB(0, 130, 220)
    end)
end

-- 5. Danh sách tính năng trong mục Hỗ trợ
local supportList = {
    {
        Name = "Spider Script",
        Func = function()
            loadstring(game:HttpGet("https://pastefy.app/wa3v2Vgm/raw"))("Spider Script")
        end
    },
    {
        Name = "Vào lại Server (Rejoin)",
        Func = function()
            game:GetService("TeleportService"):Teleport(game.PlaceId, game.Players.LocalPlayer)
        end
    },
    {
        Name = "Đổi Server khác (Server Hop)",
        Func = function()
            local TeleportService = game:GetService("TeleportService")
            local HttpService = game:GetService("HttpService")
            local Api = "https://games.roblox.com/v1/games/" .. game.PlaceId .. "/servers/0?sortOrder=Desc&limit=100"
            local success, result = pcall(function()
                return HttpService:JSONDecode(game:HttpGet(Api))
            end)
            if success and result and result.data then
                for _, s in ipairs(result.data) do
                    if type(s) == "table" and s.playing < s.maxPlayers and s.id ~= game.JobId then
                        TeleportService:TeleportToPlaceInstance(game.PlaceId, s.id)
                        break
                    end
                end
            end
        end
    },
    {
        Name = "Giảm Lag (FPS Booster)",
        Func = function()
            for _, v in pairs(game:GetDescendants()) do
                if v:IsA("Part") or v:IsA("MeshPart") then
                    v.Material = Enum.Material.SmoothPlastic
                elseif v:IsA("Decal") or v:IsA("Texture") then
                    v:Destroy()
                end
            end
        end
    },
    {
        Name = "Copy Link Discord Thọ Hub",
        Func = function()
            if setclipboard then
                setclipboard("https://discord.gg/thohub")
            end
        end
    }
}

for _, item in ipairs(supportList) do
    local ItemFrame = Instance.new("Frame")
    ItemFrame.Size = UDim2.new(1, -10, 0, 36)
    ItemFrame.BackgroundColor3 = Color3.fromRGB(22, 30, 45)
    ItemFrame.Parent = SupportContainer

    local ItemCorner = Instance.new("UICorner")
    ItemCorner.CornerRadius = UDim.new(0, 6)
    ItemCorner.Parent = ItemFrame

    local Label = Instance.new("TextLabel")
    Label.Size = UDim2.new(1, -110, 1, 0)
    Label.Position = UDim2.new(0, 12, 0, 0)
    Label.BackgroundTransparency = 1
    Label.Text = item.Name
    Label.TextColor3 = Color3.fromRGB(220, 235, 255)
    Label.Font = Enum.Font.SourceSansSemibold
    Label.TextSize = 14
    Label.TextXAlignment = Enum.TextXAlignment.Left
    Label.Parent = ItemFrame

    local ActionBtn = Instance.new("TextButton")
    ActionBtn.Size = UDim2.new(0, 90, 0, 26)
    ActionBtn.Position = UDim2.new(1, -96, 0.5, -13)
    ActionBtn.BackgroundColor3 = Color3.fromRGB(30, 80, 140)
    ActionBtn.Text = "Kích hoạt"
    ActionBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    ActionBtn.Font = Enum.Font.SourceSansBold
    ActionBtn.TextSize = 13
    ActionBtn.Parent = ItemFrame

    local ActionCorner = Instance.new("UICorner")
    ActionCorner.CornerRadius = UDim.new(0, 5)
    ActionCorner.Parent = ActionBtn

    ActionBtn.MouseButton1Click:Connect(function()
        pcall(item.Func)
        ActionBtn.Text = "Xong!"
        ActionBtn.BackgroundColor3 = Color3.fromRGB(0, 180, 120)
        task.wait(1.5)
        ActionBtn.Text = "Kích hoạt"
        ActionBtn.BackgroundColor3 = Color3.fromRGB(30, 80, 140)
    end)
end

-- 6. Xử lý Chuyển Tab
TabScriptBtn.MouseButton1Click:Connect(function()
    TabScriptBtn.BackgroundColor3 = Color3.fromRGB(0, 130, 220)
    TabScriptBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    TabSupportBtn.BackgroundColor3 = Color3.fromRGB(25, 35, 50)
    TabSupportBtn.TextColor3 = Color3.fromRGB(180, 200, 220)

    ScriptContainer.Visible = true
    SupportContainer.Visible = false
end)

TabSupportBtn.MouseButton1Click:Connect(function()
    TabSupportBtn.BackgroundColor3 = Color3.fromRGB(0, 130, 220)
    TabSupportBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    TabScriptBtn.BackgroundColor3 = Color3.fromRGB(25, 35, 50)
    TabScriptBtn.TextColor3 = Color3.fromRGB(180, 200, 220)

    ScriptContainer.Visible = false
    SupportContainer.Visible = true
end)

-- 7. Xử lý Đóng / Thu nhỏ
local isMinimized = false

MinimizeBtn.MouseButton1Click:Connect(function()
    isMinimized = not isMinimized
    if isMinimized then
        TabBar.Visible = false
        ScriptContainer.Visible = false
        SupportContainer.Visible = false
        MainFrame:TweenSize(UDim2.new(0, 420, 0, 45), Enum.EasingDirection.Out, Enum.EasingStyle.Quart, 0.2, true)
        MinimizeBtn.Text = "+"
    else
        MainFrame:TweenSize(UDim2.new(0, 420, 0, 400), Enum.EasingDirection.Out, Enum.EasingStyle.Quart, 0.2, true)
        task.wait(0.15)
        TabBar.Visible = true
        if TabScriptBtn.BackgroundColor3 == Color3.fromRGB(0, 130, 220) then
            ScriptContainer.Visible = true
        else
            SupportContainer.Visible = true
        end
        MinimizeBtn.Text = "-"
    end
end)

CloseBtn.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)
