# Pjscriptsfarmmain-- Auto Farm Script para Blox Fruits
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local workspace = game:GetService("Workspace")
local replicatedStorage = game:GetService("ReplicatedStorage")

-- Função para mover o personagem até um NPC
function moveToNpc(npc)
    local targetPosition = npc.HumanoidRootPart.Position
    character:MoveTo(targetPosition)
    
    -- Aguarda até que o personagem chegue no NPC
    while (character.HumanoidRootPart.Position - targetPosition).Magnitude > 5 do
        wait(1)
    end
end

-- Função para completar uma missão
function completeMission(npc)
    if npc:FindFirstChild("Mission") then
        local mission = npc.Mission
        print("Missão iniciada: " .. mission.Name)
        
        -- Simula a conclusão da missão (aqui você pode ajustar com base no seu sistema de missões)
        wait(mission.CompletionTime)  -- Ajuste o tempo conforme necessário
        
        print("Missão completada: " .. mission.Name)
    end
end

-- Função para realizar o Auto Farm em uma ilha
function autoFarmIsland(island)
    -- Itera sobre todos os NPCs na ilha
    for _, npc in pairs(island:GetChildren()) do
        if npc:FindFirstChild("HumanoidRootPart") then
            moveToNpc(npc)
            completeMission(npc)
        end
    end
end

-- Função principal de Auto Farm para todas as ilhas
function autoFarmAllIslands()
    local islands = workspace.Islands:GetChildren()
    
    while true do
        for _, island in pairs(islands) do
            -- Realiza o Auto Farm em cada ilha
            autoFarmIsland(island)
            
            -- Pausa entre as ilhas para evitar sobrecarga
            wait(5)
        end
        -- Repete o ciclo de farm
        wait(10)
    end
end

-- Inicia o Auto Farm para todas as ilhas
autoFarmAllIslands()
