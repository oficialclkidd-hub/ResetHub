-- 🔐 KEY SYSTEM
local CORRECT_KEY = "ResetHub"
local player = game.Players.LocalPlayer

local enteredKey = ""

-- UI simples de key
local KeyGui = Instance.new("ScreenGui")
KeyGui.Name = "KeySystem"
KeyGui.Parent = player:WaitForChild("PlayerGui")

local Frame = Instance.new("Frame", KeyGui)
Frame.Size = UDim2.fromOffset(300, 160)
Frame.Position = UDim2.fromScale(0.5, 0.5)
Frame.AnchorPoint = Vector2.new(0.5, 0.5)
Frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)

local UICorner = Instance.new("UICorner", Frame)

local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1, 0, 0, 40)
Title.Text = "🔐 Reset Hub - Key System"
Title.TextColor3 = Color3.new(1,1,1)
Title.BackgroundTransparency = 1
Title.Font = Enum.Font.GothamBold
Title.TextSize = 14

local TextBox = Instance.new("TextBox", Frame)
TextBox.PlaceholderText = "Digite a key aqui"
TextBox.Size = UDim2.new(1, -20, 0, 40)
TextBox.Position = UDim2.fromOffset(10, 50)
TextBox.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
TextBox.TextColor3 = Color3.new(1,1,1)
TextBox.Font = Enum.Font.Gotham
TextBox.TextSize = 14
Instance.new("UICorner", TextBox)

local Button = Instance.new("TextButton", Frame)
Button.Size = UDim2.new(1, -20, 0, 40)
Button.Position = UDim2.fromOffset(10, 100)
Button.Text = "Verificar Key"
Button.BackgroundColor3 = Color3.fromRGB(170, 0, 0)
Button.TextColor3 = Color3.new(1,1,1)
Button.Font = Enum.Font.GothamBold
Button.TextSize = 14
Instance.new("UICorner", Button)

Button.MouseButton1Click:Connect(function()
    if TextBox.Text == CORRECT_KEY then
        KeyGui:Destroy()

        -- 🚀 SCRIPT PRINCIPAL
        local WindUI = loadstring(game:HttpGet(
            "https://github.com/Footagesus/WindUI/releases/latest/download/main.lua"
        ))()

        local Window = WindUI:CreateWindow({
            Title = "Reset Hub [Teste]",
            Icon = "shield",
            Author = "by c00lkidd",
            Folder = "MyResetHub",
            Size = UDim2.fromOffset(580, 460),
            MinSize = Vector2.new(560, 350),
            MaxSize = Vector2.new(850, 560),
            Transparent = true,
            Theme = "Red",
            Resizable = true,
            SideBarWidth = 200,
            BackgroundImageTransparency = 0.42,
            HideSearchBar = true,
            ScrollBarEnabled = false,
        })

        -- 🏠 TAB PRINCIPAL
        local MainTab = Window:Tab({
            Title = "🏠 Principal",
            Icon = "home"
        })

        MainTab:Toggle({
            Title = "⚡ Velocidade (Speed Hack)",
            Default = false,
            Callback = function(v)
                local char = player.Character or player.CharacterAdded:Wait()
                local hum = char:FindFirstChildOfClass("Humanoid")
                if hum then
                    hum.WalkSpeed = v and 100 or 16
                end
            end
        })

        MainTab:Button({
            Title = "🔄 Rejoin no servidor",
            Callback = function()
                game:GetService("TeleportService"):Teleport(
                    game.PlaceId,
                    player
                )
            end
        })

        -- 🔔 NOTIFICAÇÃO
        WindUI:Notify({
            Title = "👋 Bem-vindo ao Reset Hub",
            Content = "Key correta! Script ativado.",
            Duration = 6,
            Image = "success"
        })

        -- 💳 TAB CRÉDITOS
        local CreditsTab = Window:Tab({
            Title = "💳 Créditos",
            Icon = "credit-card"
        })

        CreditsTab:Button({
            Title = "📜 Ver créditos do script",
            Callback = function()
                WindUI:Notify({
                    Title = "💳 Créditos do Reset Hub",
                    Content =
                        "👑 Dono: c00lkidd\n" ..
                        "⭐ Sub-Dono: ninguém\n" ..
                        "🛡 Administrador: ninguém\n" ..
                        "⚔ Moderador: ninguém\n" ..
                        "⚒ Staff: ninguém\n" ..
                        "🔧 Tester: ninguém",
                    Duration = 8,
                    Image = "success"
                })
            end
        })
    else
        Button.Text = "❌ Key incorreta"
        wait(1)
        Button.Text = "Verificar Key"
    end
end)
