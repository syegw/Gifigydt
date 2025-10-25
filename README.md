-- Coquette Hub Style Script
-- Criado por [Teste4]
-- Versão: 1.9

local CoquetteHub = {}

-- Configurações do Hub
CoquetteHub.Settings = {
    Nome = "Coquette Hub",
    Versao = "1.0",
    Desenvolvedor = "SeuNome",
    CorPrincipal = Color3.fromRGB(255, 182, 193), -- Rosa coquette
    CorSecundaria = Color3.fromRGB(255, 105, 180) -- Rosa mais forte
}

-- Biblioteca para criar a interface
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/bloodball/-back-ups-for-libs/main/uwuware"))()

-- Função para criar a janela principal
function CoquetteHub:Iniciar()
    local Window = Library:CreateWindow("Coquette Hub") {
        Nome = CoquetteHub.Settings.Nome,
        Conteudo = "Bem-vindo ao Coquette Hub! 💕"
    }

    -- Aba Principal
    local MainTab = Window:AddTab("Principal")
    
    -- Seção de Player
    local PlayerSection = MainTab:AddSection("Player")
    
    PlayerSection:AddToggle({
        Text = "Walkspeed Aumentada",
        Callback = function(state)
            if state then
                game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 50
            else
                game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
            end
        end
    })
    
    PlayerSection:AddSlider({
        Text = "Velocidade",
        Default = 16,
        Minimum = 16,
        Maximum = 100,
        Callback = function(value)
            game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = value
        end
    })
    
    PlayerSection:AddToggle({
        Text = "JumpPower Aumentada",
        Callback = function(state)
            if state then
                game.Players.LocalPlayer.Character.Humanoid.JumpPower = 100
            else
                game.Players.LocalPlayer.Character.Humanoid.JumpPower = 50
            end
        end
    })

    -- Seção de Visual
    local VisualSection = MainTab:AddSection("Visual")
    
    VisualSection:AddToggle({
        Text = "ESP (Ver jogadores)",
        Callback = function(state)
            CoquetteHub:ToggleESP(state)
        end
    })
    
    VisualSection:AddToggle({
        Text = "Chams",
        Callback = function(state)
            CoquetteHub:ToggleChams(state)
        end
    })
    
    VisualSection:AddColorPicker({
        Text = "Cor do ESP",
        Default = CoquetteHub.Settings.CorPrincipal,
        Callback = function(color)
            CoquetteHub.ESPColor = color
        end
    })

    -- Aba de Scripts
    local ScriptsTab = Window:AddTab("Scripts")
    
    local GamesSection = ScriptsTab:AddSection("Jogos Populares")
    
    GamesSection:AddButton({
        Text = "Da Hood",
        Callback = function()
            loadstring(game:HttpGet("https://raw.githubusercontent.com/script/da-hood/main.lua"))()
        end
    })
    
    GamesSection:AddButton({
        Text = "Brookhaven",
        Callback = function()
            loadstring(game:HttpGet("https://raw.githubusercontent.com/script/brookhaven/main.lua"))()
        end
    })
    
    GamesSection:AddButton({
        Text = "Arsenal",
        Callback = function()
            loadstring(game:HttpGet("https://raw.githubusercontent.com/script/arsenal/main.lua"))()
        end
    })

    -- Aba de Configurações
    local SettingsTab = Window:AddTab("Configurações")
    
    local UISection = SettingsTab:AddSection("Interface")
    
    UISection:AddToggle({
        Text = "Tema Rosa",
        Default = true,
        Callback = function(state)
            CoquetteHub:ToggleTemaRosa(state)
        end
    })
    
    UISection:AddKeybind({
        Text = "Toggle UI",
        Default = "RightControl",
        Callback = function()
            Library:ToggleUI()
        end
    })
    
    local InfoSection = SettingsTab:AddSection("Informações")
    
    InfoSection:AddLabel("Versão: " .. CoquetteHub.Settings.Versao)
    InfoSection:AddLabel("Desenvolvedor: " .. CoquetteHub.Settings.Desenvolvedor)
    InfoSection:AddLabel("Jogo: " .. game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId).Name)

    -- Aba de Creditos
    local CreditsTab = Window:AddTab("Créditos")
    
    local CreditsSection = CreditsTab:AddSection("Desenvolvedores")
    
    CreditsSection:AddLabel("Desenvolvido por: " .. CoquetteHub.Settings.Desenvolvedor)
    CreditsSection:AddLabel("Agradecimentos especiais!")
    
    CreditsSection:AddButton({
        Text = "Copiar Discord",
        Callback = function()
            setclipboard("seu_discord_aqui")
        end
    })
end

-- Função ESP
function CoquetteHub:ToggleESP(state)
    if state then
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Character then
                CoquetteHub:CriarESP(player.Character)
            end
        end
    else
        -- Código para remover ESP
    end
end

-- Função Chams
function CoquetteHub:ToggleChams(state)
    if state then
        for _, player in pairs(game.Players:GetPlayers()) do
            if player ~= game.Players.LocalPlayer and player.Character then
                CoquetteHub:CriarChams(player.Character)
            end
        end
    else
        -- Código para remover Chams
    end
end

-- Função para criar ESP
function CoquetteHub:CriarESP(character)
    local highlight = Instance.new("Highlight")
    highlight.Parent = character
    highlight.FillColor = CoquetteHub.Settings.CorPrincipal
    highlight.OutlineColor = CoquetteHub.Settings.CorSecundaria
    highlight.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
end

-- Função para criar Chams
function CoquetteHub:CriarChams(character)
    for _, part in pairs(character:GetDescendants()) do
        if part:IsA("BasePart") then
            part.Material = Enum.Material.ForceField
            part.Color = CoquetteHub.Settings.CorPrincipal
        end
    end
end

-- Função para alternar tema rosa
function CoquetteHub:ToggleTemaRosa(state)
    if state then
        -- Aplicar tema rosa
    else
        -- Aplicar tema padrão
    end
end

-- Notificação de inicialização
function CoquetteHub:Notificar()
    game:GetService("StarterGui"):SetCore("SendNotification", {
        Title = CoquetteHub.Settings.Nome,
        Text = "Hub carregado com sucesso! 💖",
        Icon = "rbxassetid://0",
        Duration = 5
    })
end

-- Inicializar o script
CoquetteHub:Iniciar()
CoquetteHub:Notificar()

print("🎀 Coquette Hub carregado com sucesso!")
print("✨ Desenvolvido por: " .. CoquetteHub.Settings.Desenvolvedor)
print("📦 Versão: " .. CoquetteHub.Settings.Versao)
