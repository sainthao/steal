local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local player = Players.LocalPlayer
local savedPos, noclipEnabled, noclipConn = nil, false, nil

local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "STNGui"
gui.ResetOnSpawn = false  -- Keeps GUI after death/respawn

local function createBtn(pos, text, color)
    local b = Instance.new("TextButton", gui)
    b.Size, b.Position = UDim2.new(0,150,0,50), pos
    b.BackgroundColor3, b.Text = color, text
    return b
end

local saveBtn = createBtn(UDim2.new(0,10,0,10), "Save Position", Color3.fromRGB(0,170,255))
local teleportBtn = createBtn(UDim2.new(0,10,0,70), "Teleport", Color3.fromRGB(0,255,170))
local noclipBtn = createBtn(UDim2.new(0,10,0,130), "Enable Noclip", Color3.fromRGB(255,85,0))

local function noclip()
    if not noclipEnabled then return end
    local char = player.Character
    if char then
        for _, part in pairs(char:GetChildren()) do
            if part:IsA("BasePart") then part.CanCollide = false end
        end
    end
end

saveBtn.MouseButton1Click:Connect(function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp then
        savedPos = hrp.Position
        saveBtn.Text = "Saved!"
        wait(1)
        saveBtn.Text = "Save Position"
    end
end)

teleportBtn.MouseButton1Click:Connect(function()
    local hrp = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
    if hrp and savedPos then
        hrp.CFrame = CFrame.new(savedPos)
        teleportBtn.Text = "Teleported!"
        wait(1)
        teleportBtn.Text = "Teleport"
    end
end)

noclipBtn.MouseButton1Click:Connect(function()
    noclipEnabled = not noclipEnabled
    noclipBtn.Text = noclipEnabled and "Disable Noclip" or "Enable Noclip"
    if noclipEnabled then
        noclipConn = RunService.Stepped:Connect(noclip)
    else
        if noclipConn then noclipConn:Disconnect() noclipConn = nil end
        local char = player.Character
        if char then
            for _, part in pairs(char:GetChildren()) do
                if part:IsA("BasePart") then part.CanCollide = true end
            end
        end
    end
end)

player.CharacterAdded:Connect(function()
    wait(1)
    if noclipEnabled then noclip() end
end)
