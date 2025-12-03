local TweenService = game:GetService("TweenService")

local function applyAdidasWalk(char)
    local humanoid = char:WaitForChild("Humanoid")

    -- Desliga animação padrão de andar
    humanoid.WalkSpeed = 10
    humanoid.AutoRotate = false

    -- Cria loop de balanço estilo "Adidas"
    task.spawn(function()
        while char and humanoid.Health > 0 do
            local root = char:FindFirstChild("HumanoidRootPart")
            if not root then break end

            -- Balanço pra esquerda
            local goal1 = {CFrame = root.CFrame * CFrame.Angles(0, 0, math.rad(10))}
            local t1 = TweenService:Create(root, TweenInfo.new(0.25, Enum.EasingStyle.Sine), goal1)
            t1:Play()
            t1.Completed:Wait()

            -- Balanço pra direita
            local goal2 = {CFrame = root.CFrame * CFrame.Angles(0, 0, math.rad(-10))}
            local t2 = TweenService:Create(root, TweenInfo.new(0.25, Enum.EasingStyle.Sine), goal2)
            t2:Play()
            t2.Completed:Wait()
        end
    end)
end

-- Aplica quando jogador nascer
game.Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function(char)
        task.wait(1)
        applyAdidasWalk(char)
    end)
end)
