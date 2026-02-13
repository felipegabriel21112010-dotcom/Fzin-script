-- FZIN HUB - Tsunami for Brainrots (OTIMIZADO)
-- Créditos: @fzin_scripts

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "FzinHub"
ScreenGui.Parent = game.CoreGui
ScreenGui.ResetOnSpawn = false

-- === SISTEMA DE KEY ===
local function isValidKey(key)
    return string.match(key, "^FZIN%-X%w%w%w%-%w%w%w%w%-%w%w%w%w$") ~= nil
end

-- Frame da Key
local KeyFrame = Instance.new("Frame")
KeyFrame.Name = "KeyFrame"
KeyFrame.Parent = ScreenGui
KeyFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
KeyFrame.Position = UDim2.new(0.5, -180, 0.5, -120)
KeyFrame.Size = UDim2.new(0, 360, 0, 240)
KeyFrame.BorderSizePixel = 0
KeyFrame.Active = true
KeyFrame.Draggable = true

local KeyCorner = Instance.new("UICorner")
KeyCorner.CornerRadius = UDim.new(0, 14)
KeyCorner.Parent = KeyFrame

local KeyTitle = Instance.new("TextLabel")
KeyTitle.Parent = KeyFrame
KeyTitle.BackgroundTransparency = 1
KeyTitle.Size = UDim2.new(1, 0, 0, 50)
KeyTitle.Font = Enum.Font.SourceSansBold
KeyTitle.Text = "FZIN HUB - KEY"
KeyTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
KeyTitle.TextSize = 22

local KeyBox = Instance.new("TextBox")
KeyBox.Parent = KeyFrame
KeyBox.Position = UDim2.new(0.5, -150, 0, 80)
KeyBox.Size = UDim2.new(0, 300, 0, 40)
KeyBox.BackgroundColor3 = Color3.fromRGB(26, 26, 26)
KeyBox.Text = ""
KeyBox.PlaceholderText = "Digite sua key 🔑"
KeyBox.TextColor3 = Color3.fromRGB(255,255,255)
KeyBox.PlaceholderColor3 = Color3.fromRGB(150,150,150)
KeyBox.Font = Enum.Font.SourceSans
KeyBox.TextSize = 18
KeyBox.ClearTextOnFocus = false
KeyBox.BorderSizePixel = 0

local KeyBoxCorner = Instance.new("UICorner")
KeyBoxCorner.CornerRadius = UDim.new(0, 10)
KeyBoxCorner.Parent = KeyBox

local ConfirmBtn = Instance.new("TextButton")
ConfirmBtn.Parent = KeyFrame
ConfirmBtn.Position = UDim2.new(0.5, -100, 0, 140)
ConfirmBtn.Size = UDim2.new(0, 200, 0, 40)
ConfirmBtn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
ConfirmBtn.Text = "Confirmar"
ConfirmBtn.TextColor3 = Color3.fromRGB(255,255,255)
ConfirmBtn.Font = Enum.Font.SourceSansBold
ConfirmBtn.TextSize = 18
ConfirmBtn.BorderSizePixel = 0

local ConfirmCorner = Instance.new("UICorner")
ConfirmCorner.CornerRadius = UDim.new(0, 10)
ConfirmCorner.Parent = ConfirmBtn

local StatusLabel = Instance.new("TextLabel")
StatusLabel.Parent = KeyFrame
StatusLabel.BackgroundTransparency = 1
StatusLabel.Position = UDim2.new(0, 0, 1, -40)
StatusLabel.Size = UDim2.new(1, 0, 0, 30)
StatusLabel.Font = Enum.Font.SourceSans
StatusLabel.Text = ""
StatusLabel.TextColor3 = Color3.fromRGB(255, 80, 80)
StatusLabel.TextSize = 14

-- === MENU PRINCIPAL ===
local MainFrame = Instance.new("Frame")
local Header = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local MinimizeBtn = Instance.new("TextButton")
local CloseBtn = Instance.new("TextButton")
local TabsFrame = Instance.new("Frame")
local ContentFrame = Instance.new("Frame")
local Footer = Instance.new("TextLabel")
local MiniMenu = Instance.new("TextButton")

-- Variáveis de Estado
local currentTab = "Main"
local animSpeed = 2
local States = {
    Godmode = false,
    Vip = false,
    Fly = false,
    Speed = false,
    InfJump = false,
    EspPlayers = false,
    EspCelestial = false,
    EspDivines = false,
    EspAll = false
}

-- Mini Menu Setup
MiniMenu.Name = "MiniMenu"
MiniMenu.Parent = ScreenGui
MiniMenu.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MiniMenu.Position = UDim2.new(0.5, -50, 0.05, 0)
MiniMenu.Size = UDim2.new(0, 100, 0, 40)
MiniMenu.Visible = false
MiniMenu.Font = Enum.Font.SourceSansBold
MiniMenu.Text = "FZIN HUB"
MiniMenu.TextColor3 = Color3.fromRGB(255, 255, 255)
MiniMenu.TextSize = 18
local MiniCorner = Instance.new("UICorner")
MiniCorner.CornerRadius = UDim.new(0, 12)
MiniCorner.Parent = MiniMenu

-- Main Frame Setup
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.Position = UDim2.new(0.5, -210, 0.5, -175)
MainFrame.Size = UDim2.new(0, 420, 0, 400)
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.BorderSizePixel = 0
MainFrame.Visible = false
local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 14)
MainCorner.Parent = MainFrame

-- Header
Header.Name = "Header"
Header.Parent = MainFrame
Header.BackgroundColor3 = Color3.fromRGB(16, 16, 16)
Header.Size = UDim2.new(1, 0, 0, 45)
Header.BorderSizePixel = 0
local HeaderCorner = Instance.new("UICorner")
HeaderCorner.CornerRadius = UDim.new(0, 14)
HeaderCorner.Parent = Header

Title.Name = "Title"
Title.Parent = Header
Title.BackgroundTransparency = 1
Title.Position = UDim2.new(0, 15, 0, 0)
Title.Size = UDim2.new(0, 200, 1, 0)
Title.Font = Enum.Font.SourceSansBold
Title.Text = "FZIN HUB"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 20
Title.TextXAlignment = Enum.TextXAlignment.Left

-- Botões de controle
CloseBtn.Name = "CloseBtn"
CloseBtn.Parent = Header
CloseBtn.BackgroundColor3 = Color3.fromRGB(28, 28, 28)
CloseBtn.Position = UDim2.new(1, -36, 0.5, -13)
CloseBtn.Size = UDim2.new(0, 26, 0, 26)
CloseBtn.Font = Enum.Font.SourceSansBold
CloseBtn.Text = "X"
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.TextSize = 18
CloseBtn.BorderSizePixel = 0
local ClsCorner = Instance.new("UICorner")
ClsCorner.CornerRadius = UDim.new(0, 6)
ClsCorner.Parent = CloseBtn

MinimizeBtn.Name = "MinimizeBtn"
MinimizeBtn.Parent = Header
MinimizeBtn.BackgroundColor3 = Color3.fromRGB(28, 28, 28)
MinimizeBtn.Position = UDim2.new(1, -68, 0.5, -13)
MinimizeBtn.Size = UDim2.new(0, 26, 0, 26)
MinimizeBtn.Font = Enum.Font.SourceSansBold
MinimizeBtn.Text = "-"
MinimizeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeBtn.TextSize = 20
MinimizeBtn.BorderSizePixel = 0
local MinCorner = Instance.new("UICorner")
MinCorner.CornerRadius = UDim.new(0, 6)
MinCorner.Parent = MinimizeBtn

-- Tabs
TabsFrame.Name = "Tabs"
TabsFrame.Parent = MainFrame
TabsFrame.BackgroundColor3 = Color3.fromRGB(17, 17, 17)
TabsFrame.Position = UDim2.new(0, 0, 0, 45)
TabsFrame.Size = UDim2.new(1, 0, 0, 40)
TabsFrame.BorderSizePixel = 0

local function createTab(name, pos)
    local tab = Instance.new("TextButton")
    tab.Name = name .. "Tab"
    tab.Parent = TabsFrame
    tab.BackgroundColor3 = Color3.fromRGB(17, 17, 17)
    tab.Position = UDim2.new(pos, 0, 0, 0)
    tab.Size = UDim2.new(0.333, 0, 1, 0)
    tab.Font = Enum.Font.SourceSansBold
    tab.Text = name:upper()
    tab.TextColor3 = (name == "Main") and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(170, 170, 170)
    tab.TextSize = 16
    tab.BorderSizePixel = 0
    local underline = Instance.new("Frame")
    underline.Name = "Underline"
    underline.Parent = tab
    underline.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    underline.Position = UDim2.new(0, 0, 1, -2)
    underline.Size = UDim2.new(1, 0, 0, 2)
    underline.Visible = (name == "Main")
    underline.BorderSizePixel = 0
    return tab
end

local MainTab = createTab("Main", 0)
local VisualTab = createTab("Esp", 0.333)
local ConfigTab = createTab("Config", 0.666)

-- Content
ContentFrame.Name = "Content"
ContentFrame.Parent = MainFrame
ContentFrame.BackgroundTransparency = 1
ContentFrame.Position = UDim2.new(0, 14, 0, 95)
ContentFrame.Size = UDim2.new(1, -28, 1, -145)

local Sections = {}
local function createSection(name)
    local section = Instance.new("Frame")
    section.Name = name
    section.Parent = ContentFrame
    section.BackgroundTransparency = 1
    section.Size = UDim2.new(1, 0, 1, 0)
    section.Visible = (name == "Main")
    section.BorderSizePixel = 0
    local layout = Instance.new("UIListLayout")
    layout.Parent = section
    layout.Padding = UDim.new(0, 8)
    Sections[name] = section
    return section
end

local MainSection = createSection("Main")
local VisualSection = createSection("Esp")
local ConfigSection = createSection("Config")

-- Footer
Footer.Name = "Footer"
Footer.Parent = MainFrame
Footer.BackgroundColor3 = Color3.fromRGB(16, 16, 16)
Footer.Position = UDim2.new(0, 0, 1, -35)
Footer.Size = UDim2.new(1, 0, 0, 35)
Footer.Font = Enum.Font.SourceSans
Footer.Text = "Créditos: @fzin_scripts"
Footer.TextColor3 = Color3.fromRGB(170, 170, 170)
Footer.TextSize = 12
Footer.BorderSizePixel = 0
local FooterCorner = Instance.new("UICorner")
FooterCorner.CornerRadius = UDim.new(0, 14)
FooterCorner.Parent = Footer

-- === FUNÇÕES LÓGICAS (GAMEPLAY) ===

-- Função de ESP (Aura + Nome)
local function createESP(object, color, name)
    if not object or not object:IsA("Model") then return end
    if object:FindFirstChild("TsunamiESP") then return end
    
    local highlight = Instance.new("Highlight")
    highlight.Name = "TsunamiESP"
    highlight.Parent = object
    highlight.FillColor = color
    highlight.OutlineColor = Color3.new(1, 1, 1)
    highlight.FillTransparency = 0.5
    highlight.OutlineTransparency = 0
    highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop

    if name then
        local billboard = Instance.new("BillboardGui")
        billboard.Name = "TsunamiName"
        billboard.Parent = object
        billboard.AlwaysOnTop = true
        billboard.Size = UDim2.new(0, 200, 0, 50)
        billboard.ExtentsOffset = Vector3.new(0, 3, 0)
        
        local label = Instance.new("TextLabel")
        label.Parent = billboard
        label.BackgroundTransparency = 1
        label.Size = UDim2.new(1, 0, 1, 0)
        label.Text = name
        label.TextColor3 = color
        label.Font = Enum.Font.SourceSansBold
        label.TextSize = 14
        label.TextStrokeTransparency = 0
    end
end

local function removeESP(object)
    if not object then return end
    if object:FindFirstChild("TsunamiESP") then object.TsunamiESP:Destroy() end
    if object:FindFirstChild("TsunamiName") then object.TsunamiName:Destroy() end
end

-- Loop de ESP Otimizado
RunService.RenderStepped:Connect(function()
    -- ESP Players
    for _, player in pairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            if States.EspPlayers then
                createESP(player.Character, Color3.new(1, 0, 0), player.Name)
            else
                removeESP(player.Character)
            end
        end
    end

    -- ESP Brainrots por Classificação
    for _, obj in pairs(workspace:GetDescendants()) do
        if obj:IsA("Model") and (obj:FindFirstChild("Humanoid") or obj:FindFirstChild("HumanoidRootPart")) then
            local isBrainrot = obj.Name:lower():find("brainrot") or obj:FindFirstChild("Rarity")
            if isBrainrot then
                local rarityValue = obj:FindFirstChild("Rarity") and obj.Rarity.Value or "Normal"
                local color = Color3.new(1, 1, 1)
                local show = false
                
                if rarityValue == "Celestial" then
                    color = Color3.fromRGB(255, 215, 0)
                    show = States.EspCelestial or States.EspAll
                elseif rarityValue == "Divine" or rarityValue == "Godly" then
                    color = Color3.fromRGB(255, 0, 255)
                    show = States.EspDivines or States.EspAll
                elseif rarityValue == "Mythical" then
                    color = Color3.fromRGB(255, 0, 0)
                    show = States.EspAll
                elseif rarityValue == "Legendary" then
                    color = Color3.fromRGB(255, 165, 0)
                    show = States.EspAll
                else
                    show = States.EspAll
                end
                
                if show then
                    createESP(obj, color, rarityValue:upper())
                else
                    if not States.EspPlayers or not obj:IsDescendantOf(workspace) then 
                        removeESP(obj) 
                    end
                end
            end
        end
    end
end)

-- Godmode Estável
RunService.Heartbeat:Connect(function()
    if States.Godmode and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
        local hum = LocalPlayer.Character.Humanoid
        hum.Health = hum.MaxHealth
        -- Proteção contra queda no void
        if LocalPlayer.Character.PrimaryPart and LocalPlayer.Character.PrimaryPart.Position.Y < -500 then
            LocalPlayer.Character.PrimaryPart.CFrame = CFrame.new(0, 100, 0)
        end
    end
end)

-- Fly Aprimorado (Sem Bugs)
local flySpeed = 50
local bv, bg
RunService.RenderStepped:Connect(function()
    if States.Fly and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        local hrp = LocalPlayer.Character.HumanoidRootPart
        if not bv then
            bv = Instance.new("BodyVelocity", hrp)
            bv.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
            bv.Velocity = Vector3.new(0, 0, 0)
            bg = Instance.new("BodyGyro", hrp)
            bg.MaxTorque = Vector3.new(math.huge, math.huge, math.huge)
            bg.CFrame = hrp.CFrame
        end
        
        local cam = workspace.CurrentCamera
        local direction = Vector3.new(0, 0, 0)
        
        if UserInputService:IsKeyDown(Enum.KeyCode.W) then direction = direction + cam.CFrame.LookVector end
        if UserInputService:IsKeyDown(Enum.KeyCode.S) then direction = direction - cam.CFrame.LookVector end
        if UserInputService:IsKeyDown(Enum.KeyCode.A) then direction = direction - cam.CFrame.RightVector end
        if UserInputService:IsKeyDown(Enum.KeyCode.D) then direction = direction + cam.CFrame.RightVector end
        if UserInputService:IsKeyDown(Enum.KeyCode.Space) then direction = direction + Vector3.new(0, 1, 0) end
        if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) then direction = direction - Vector3.new(0, 1, 0) end
        
        bv.Velocity = direction * flySpeed
        bg.CFrame = cam.CFrame
        LocalPlayer.Character.Humanoid.PlatformStand = true
    else
        if bv then bv:Destroy() bv = nil end
        if bg then bg:Destroy() bg = nil end
        if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
            LocalPlayer.Character.Humanoid.PlatformStand = false
        end
    end
end)

-- Infinite Jump
UserInputService.JumpRequest:Connect(function()
    if States.InfJump and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
        LocalPlayer.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
    end
end)

-- Speed Loop
RunService.Heartbeat:Connect(function()
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
        if States.Speed then
            LocalPlayer.Character.Humanoid.WalkSpeed = 100
        else
            LocalPlayer.Character.Humanoid.WalkSpeed = 16
        end
    end
end)

-- VIP & Godmode (NoWall)
local function updateWorld()
    for _, obj in pairs(workspace:GetDescendants()) do
        if States.Godmode and (obj.Name:lower():find("wall") or obj.Name:lower():find("parede")) and obj:IsA("BasePart") then
            obj.CanCollide = false
            obj.Transparency = 0.5
        end
        if States.Vip and (obj.Name:lower():find("vip") or obj.Name:lower():find("premium")) and obj:IsA("BasePart") then
            obj.CanCollide = false
            obj.Transparency = 0.8
        end
    end
end

-- === FUNÇÃO DE TELEPORTE PARA SPAWN ===
local function teleportToSpawn()
    if LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
        local spawnLocation = workspace:FindFirstChild("SpawnLocation") or workspace:FindFirstChildOfClass("SpawnLocation")
        if spawnLocation then
            LocalPlayer.Character.HumanoidRootPart.CFrame = spawnLocation.CFrame + Vector3.new(0, 5, 0)
        else
            LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, 50, 0)
        end
    end
end

-- === BOTÕES DE FUNÇÃO ===
local function applyRGB(button)
    local connection
    connection = RunService.RenderStepped:Connect(function()
        if not button:GetAttribute("Selected") then 
            connection:Disconnect()
            button.BackgroundColor3 = Color3.fromRGB(26, 26, 26)
            button.TextColor3 = Color3.fromRGB(255, 255, 255)
            return 
        end
        local t = (tick() % animSpeed) / animSpeed
        local colorVal = (t < 0.5) and (t * 2) or (2 - (t * 2))
        button.BackgroundColor3 = Color3.new(colorVal, colorVal, colorVal)
        button.TextColor3 = Color3.new(1-colorVal, 1-colorVal, 1-colorVal)
    end)
end

local function createFunctionButton(parent, text, stateKey)
    local btn = Instance.new("TextButton")
    btn.Name = text
    btn.Parent = parent
    btn.BackgroundColor3 = Color3.fromRGB(26, 26, 26)
    btn.Size = UDim2.new(1, 0, 0, 38)
    btn.Font = Enum.Font.SourceSans
    btn.Text = "  " .. text
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize = 16
    btn.TextXAlignment = Enum.TextXAlignment.Left
    btn.BorderSizePixel = 0
    local btnCorner = Instance.new("UICorner")
    btnCorner.CornerRadius = UDim.new(0, 10)
    btnCorner.Parent = btn
    local btnStroke = Instance.new("UIStroke")
    btnStroke.Color = Color3.fromRGB(38, 38, 38)
    btnStroke.Thickness = 1
    btnStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
    btnStroke.Parent = btn

    btn.MouseButton1Click:Connect(function()
        local isSelected = not btn:GetAttribute("Selected")
        btn:SetAttribute("Selected", isSelected)
        States[stateKey] = isSelected
        
        if isSelected then
            btnStroke.Color = Color3.fromRGB(255, 255, 255)
            applyRGB(btn)
            if stateKey == "Vip" or stateKey == "Godmode" then updateWorld() end
        else
            btnStroke.Color = Color3.fromRGB(38, 38, 38)
        end
    end)
end

local function createActionButton(parent, text, callback)
    local btn = Instance.new("TextButton")
    btn.Name = text
    btn.Parent = parent
    btn.BackgroundColor3 = Color3.fromRGB(26, 26, 26)
    btn.Size = UDim2.new(1, 0, 0, 38)
    btn.Font = Enum.Font.SourceSans
    btn.Text = "  " .. text
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize = 16
    btn.TextXAlignment = Enum.TextXAlignment.Left
    btn.BorderSizePixel = 0
    local btnCorner = Instance.new("UICorner")
    btnCorner.CornerRadius = UDim.new(0, 10)
    btnCorner.Parent = btn
    local btnStroke = Instance.new("UIStroke")
    btnStroke.Color = Color3.fromRGB(38, 38, 38)
    btnStroke.Thickness = 1
    btnStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
    btnStroke.Parent = btn

    btn.MouseButton1Click:Connect(function()
        btnStroke.Color = Color3.fromRGB(255, 255, 255)
        btn.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
        callback()
        task.wait(0.2)
        btnStroke.Color = Color3.fromRGB(38, 38, 38)
        btn.BackgroundColor3 = Color3.fromRGB(26, 26, 26)
    end)
end

-- Registro de Botões
createFunctionButton(MainSection, "GOD MODE", "Godmode")
createFunctionButton(MainSection, "VIP", "Vip")
createFunctionButton(MainSection, "FLY", "Fly")
createFunctionButton(MainSection, "SPEED", "Speed")
createFunctionButton(MainSection, "INFINITE JUMP", "InfJump")
createActionButton(MainSection, "TELEPORT", teleportToSpawn)

createFunctionButton(VisualSection, "ESP PLAYERS", "EspPlayers")
createFunctionButton(VisualSection, "ESP CELESTIAL", "EspCelestial")
createFunctionButton(VisualSection, "ESP DIVINES", "EspDivines")
createFunctionButton(VisualSection, "ESP ALL", "EspAll")

-- Configurações de Cor
local function createConfigItem(text)
    local frame = Instance.new("Frame")
    frame.BackgroundColor3 = Color3.fromRGB(26, 26, 26)
