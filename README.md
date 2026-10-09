-- Services
local CoreGui = game:GetService("CoreGui")

-- Destruir GUI anterior se existir
if CoreGui:FindFirstChild("GameBoyXAnimesCodeGui") then
    CoreGui.GameBoyXAnimesCodeGui:Destroy()
end

-- ScreenGui Principal
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "GameBoyXAnimesCodeGui"
ScreenGui.ResetOnSpawn = false

if syn and syn.protect_gui then
    syn.protect_gui(ScreenGui)
    ScreenGui.Parent = CoreGui
elseif gethui then
    ScreenGui.Parent = gethui()
else
    ScreenGui.Parent = CoreGui
end

----------------------------------------------------
-- BOTÃO FLUTUANTE (BOLINHA MOVÍVEL "ANIME")
----------------------------------------------------
local ToggleButton = Instance.new("TextButton")
local UICornerBtn = Instance.new("UICorner")
local UIStrokeBtn = Instance.new("UIStroke")

ToggleButton.Name = "ToggleButton"
ToggleButton.Size = UDim2.new(0, 65, 0, 65)
ToggleButton.Position = UDim2.new(0.05, 0, 0.4, 0)
ToggleButton.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
ToggleButton.Active = true
ToggleButton.Draggable = true
ToggleButton.Text = "Anime"
ToggleButton.TextColor3 = Color3.fromRGB(85, 255, 0)
ToggleButton.Font = Enum.Font.SourceSansBold
ToggleButton.TextSize = 15
ToggleButton.Parent = ScreenGui

UICornerBtn.CornerRadius = UDim.new(1, 0)
UICornerBtn.Parent = ToggleButton

UIStrokeBtn.Color = Color3.fromRGB(85, 255, 0)
UIStrokeBtn.Thickness = 3
UIStrokeBtn.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
UIStrokeBtn.Parent = ToggleButton

----------------------------------------------------
-- PAINEL PRINCIPAL (GAMEBOYX ANIMES)
----------------------------------------------------
local MainFrame = Instance.new("Frame")
local UICornerMain = Instance.new("UICorner")
local UIStrokeMain = Instance.new("UIStroke")
local Title = Instance.new("TextLabel")
local CloseButton = Instance.new("TextButton")

MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 360, 0, 220)
MainFrame.Position = UDim2.new(0.5, -180, 0.5, -110)
MainFrame.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
MainFrame.Visible = true
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

UICornerMain.CornerRadius = UDim.new(0, 16)
UICornerMain.Parent = MainFrame

UIStrokeMain.Color = Color3.fromRGB(85, 255, 0)
UIStrokeMain.Thickness = 2
UIStrokeMain.Parent = MainFrame

Title.Name = "Title"
Title.Size = UDim2.new(1, -50, 0, 45)
Title.Position = UDim2.new(0, 20, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "GameBoy<font color=\"rgb(85,255,0)\">X Animes</font>"
Title.RichText = true
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 22
Title.Font = Enum.Font.SourceSansBold
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Parent = MainFrame

CloseButton.Name = "CloseButton"
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -40, 0, 10)
CloseButton.BackgroundTransparency = 1
CloseButton.Text = "X"
CloseButton.TextColor3 = Color3.fromRGB(255, 85, 85)
CloseButton.TextSize = 20
CloseButton.Font = Enum.Font.SourceSansBold
CloseButton.Parent = MainFrame

----------------------------------------------------
-- CAIXA DE TEXTO (NOME DO PERSONAGEM)
----------------------------------------------------
local CodeTextBox = Instance.new("TextBox")
CodeTextBox.Name = "CodeTextBox"
CodeTextBox.Size = UDim2.new(1, -40, 0, 45)
CodeTextBox.Position = UDim2.new(0, 20, 0, 60)
CodeTextBox.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
CodeTextBox.TextColor3 = Color3.fromRGB(85, 255, 0)
CodeTextBox.PlaceholderText = "Digite o nome do personagem..."
CodeTextBox.PlaceholderColor3 = Color3.fromRGB(120, 120, 120)
CodeTextBox.Font = Enum.Font.SourceSansBold
CodeTextBox.TextSize = 16
CodeTextBox.Text = ""
CodeTextBox.ClearTextOnFocus = false
CodeTextBox.Parent = MainFrame

Instance.new("UICorner", CodeTextBox).CornerRadius = UDim.new(0, 8)
local CodeBoxStroke = Instance.new("UIStroke")
CodeBoxStroke.Color = Color3.fromRGB(85, 255, 0)
CodeBoxStroke.Thickness = 1
CodeBoxStroke.Parent = CodeTextBox

----------------------------------------------------
-- BOTÃO DE EXECUTAR
----------------------------------------------------
local ExecuteBtn = Instance.new("TextButton")
ExecuteBtn.Name = "ExecuteBtn"
ExecuteBtn.Size = UDim2.new(1, -40, 0, 45)
ExecuteBtn.Position = UDim2.new(0, 20, 0, 120)
ExecuteBtn.BackgroundColor3 = Color3.fromRGB(85, 255, 0)
ExecuteBtn.Text = "⚡ EXECUTAR SCRIPT"
ExecuteBtn.TextColor3 = Color3.fromRGB(0, 0, 0)
ExecuteBtn.Font = Enum.Font.SourceSansBold
ExecuteBtn.TextSize = 16
ExecuteBtn.Parent = MainFrame

Instance.new("UICorner", ExecuteBtn).CornerRadius = UDim.new(0, 8)

-- Mensagem de Status
local StatusLabel = Instance.new("TextLabel")
StatusLabel.Name = "StatusLabel"
StatusLabel.Size = UDim2.new(1, -40, 0, 25)
StatusLabel.Position = UDim2.new(0, 20, 0, 175)
StatusLabel.BackgroundTransparency = 1
StatusLabel.Text = ""
StatusLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
StatusLabel.Font = Enum.Font.SourceSans
StatusLabel.TextSize = 14
StatusLabel.Parent = MainFrame

----------------------------------------------------
-- MAPA APENAS PELO NOME DO PERSONAGEM
----------------------------------------------------
local characterDatabase = {
    ["subaru"]     = "https://pastebin.com/raw/zsHuHzQx",
    ["reinhard"]   = "https://pastebin.com/raw/LgrwXC04",
    ["rotas"]      = "https://pastebin.com/raw/WS8fnFZQ",
    ["otto"]       = "https://pastebin.com/raw/sfG4AxUB",
    ["garfield"]   = "https://pastebin.com/raw/gQnHxNvt",
    ["garfild"]    = "https://pastebin.com/raw/gQnHxNvt",
    ["pandora"]    = "https://pastebin.com/raw/0j2Teb5k",
    ["echidna"]    = "https://pastebin.com/raw/4XqPhhTm",

    ["light"]      = "https://pastebin.com/raw/B7e6TbC8",
    ["l"]          = "https://pastebin.com/raw/P1kHEapJ",
    ["ryuk"]       = "https://pastebin.com/raw/PV2hvqPm",

    ["kaguya"]     = "https://pastebin.com/raw/PAkE1gkS",
    ["madara"]     = "https://pastebin.com/raw/3Hc2WnWv",
    ["mandara"]    = "https://pastebin.com/raw/3Hc2WnWv",
    ["minato"]     = "https://raw.githubusercontent.com/MizDrop/ScriptHub/main/MinatoDelta.lua",

    ["sakanade"]   = "https://pastebin.com/raw/1GgamUBW",
    ["ichigo"]     = "https://pastebin.com/raw/Xu7KCejS",
    ["aizen"]      = "https://pastebin.com/raw/fSaxuDSj",
    ["kisuke"]     = "https://pastebin.com/raw/kzbMMCDT",
    ["kisuki"]     = "https://pastebin.com/raw/kzbMMCDT",
    ["yoruichi"]   = "https://pastebin.com/raw/9Gtb7f0n",
    ["kido"]       = "https://pastebin.com/raw/tNu18vxd",

    ["kazuma"]     = "https://pastebin.com/raw/kpYMiYbt",
    ["megumin"]    = "https://pastebin.com/raw/1z9LRb1d",
    ["aqua"]       = "https://pastebin.com/raw/uBec3tAw",
    ["darkness"]   = "https://pastebin.com/raw/rW3tPxxb",

    ["rudeus"]     = "https://pastebin.com/raw/y3JLWuDr",
    ["fox"]        = "https://pastebin.com/raw/fMvRf2Mp",

    ["rimuru"]     = "https://pastebin.com/raw/F3MtHtd4",
    ["deku"]       = "https://pastebin.com/raw/QXzXkjTP"
}

----------------------------------------------------
-- LÓGICA DE EXECUÇÃO
----------------------------------------------------
local function runCode()
    local inputRaw = CodeTextBox.Text
    local cleanInput = string.lower(inputRaw):gsub("^%s*(.-)%s*$", "%1")

    if cleanInput == "" then
        StatusLabel.Text = "⚠️ Digite o nome de um personagem!"
        StatusLabel.TextColor3 = Color3.fromRGB(255, 200, 0)
        return
    end

    local scriptUrl = characterDatabase[cleanInput]

    if scriptUrl then
        StatusLabel.Text = "⏳ Carregando script do " .. cleanInput .. "..."
        StatusLabel.TextColor3 = Color3.fromRGB(85, 255, 0)

        task.spawn(function()
            local success, err = pcall(function()
                loadstring(game:HttpGet(scriptUrl))()
            end)

            if success then
                StatusLabel.Text = "✅ Script executado com sucesso!"
                StatusLabel.TextColor3 = Color3.fromRGB(85, 255, 0)
            else
                StatusLabel.Text = "❌ Erro ao executar o script!"
                StatusLabel.TextColor3 = Color3.fromRGB(255, 85, 85)
                warn("Erro ao executar personagem " .. cleanInput .. ": " .. tostring(err))
            end
        end)
    else
        StatusLabel.Text = "❌ Personagem não encontrado!"
        StatusLabel.TextColor3 = Color3.fromRGB(255, 85, 85)
    end
end

ExecuteBtn.MouseButton1Click:Connect(runCode)
CodeTextBox.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        runCode()
    end
end)

ToggleButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

CloseButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
end)
