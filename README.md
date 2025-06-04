local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")
local MarketplaceService = game:GetService("MarketplaceService")

local Window = Fluent:CreateWindow({
    Title = "Sensational | Tha Bronx 3",
    SubTitle = "version 69420",
    TabWidth = 160,
    Size = UDim2.fromOffset(500, 400),
    Acrylic = true,
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl
})

local Tabs = {
    Credits = Window:AddTab({ Title = "Credits", Icon = "users" }),
    Exploits = Window:AddTab({ Title = "Main", Icon = "bot" }),
    Home = Window:AddTab({ Title = "Miscellaneous", Icon = "home" }),
    Tps = Window:AddTab({ Title = "Teleports", Icon = "map" }),
    Combat = Window:AddTab({ Title = "Combat", Icon = "skull" }),
    Visual = Window:AddTab({ Title = "Visual", Icon = "eye" }),
    Bank = Window:AddTab({ Title = "Bank", Icon = "banknote" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
    
}

local Options = Fluent.Options

local function notify(title, text, time)
    Fluent:Notify({
        Title = title,
        Content = text,
        Duration = time,
        Icon = "Settings"
    })
end

local Section1 = Tabs.Credits:AddSection("Credits")
Section1:AddParagraph({
    Title = "Developers",
    Content = "Riq and Mior.\nWe are Sensational."
})

Section1:AddButton({
    Title = "Join Discord",
    Callback = function()
        setclipboard("https://discord.gg/pB4f29h2Nr")
        notify("Discord", "Discord link copied to clipboard!", 3)
    end
})
game:GetService("Players").LocalPlayer.Character.Humanoid:ChangeState(0)
local Section2 = Tabs.Tps:AddSection("Teleports")
 -- add mini pent house later :)))
local TeleportLocations = {
    { Name = "Market", Position = Vector3.new(-1241.9578999999999 + 174 + 680, 340.3467, -558.864) },
    { Name = "Pent House", Position = Vector3.new(-492.4557 + 112 + 250, 168.4685 + 251, -1422.7767 + 854) },
    { Name = "Safe", Position = Vector3.new(48917.898400000005 + 19597, 53680.5 - 396 - 343, -796.09) },
    { Name = "Dealership", Position = Vector3.new(-379.0562, 441.2626 - 188, -2614.4066000000003 + 34 + 1334) },
    { Name = "Uphill GunShop", Position = Vector3.new(66197.125, 63201.7188 + 60414, 5749.2305) },
    { Name = "Downhill GunShop", Position = Vector3.new(198909.8984 - 105940, 488.9688000000024 + 121609, 17023.8867) },
    { Name = "Laundrymat", Position = Vector3.new(-376.1771 - 601, 197.6838 + 56, -1975.5855000000001 + 1035 + 248) },
    { Name = "Bank", Position = Vector3.new(-207.377, 283.6329, -2240.6583 + 834 + 192) },
    { Name = "Construction Site", Position = Vector3.new(-3120.8307 + 135 + 1254, 1393.8123 - 1023, -5490.8387 + 4314) },
    { Name = "Backpack Shop", Position = Vector3.new(-1248.0961303710938 + 102 + 472, 253.59814453125, -684.4346313476562) },
    { Name = "Ice Box", Position = Vector3.new(-120.14073181152344 - 95, 283.5154113769531, -1173.6910400390625 - 85) },
    { Name = "Drip Shop", Position = Vector3.new(7378.695300000007 + 60084, 18630.0352 - 8141, 205.58950000000004 + 344) },
    
}

local function teleportToLocation(location)
    local player = game.Players.LocalPlayer
    if not player.Character or not player.Character:FindFirstChild("HumanoidRootPart") then
        return
    end

    local screenGui = Instance.new("ScreenGui")
    screenGui.Name = "TeleportOverlay"
    screenGui.ResetOnSpawn = false
    screenGui.Parent = game:GetService("CoreGui")

    local blackFrame = Instance.new("Frame")
    blackFrame.BackgroundColor3 = Color3.new(0, 0, 0)
    blackFrame.Size = UDim2.new(1, 0, 1, 0)
    blackFrame.BackgroundTransparency = 0
    blackFrame.BorderSizePixel = 0
    blackFrame.Parent = screenGui

    local success, err = pcall(function()
        player.Character.Humanoid:ChangeState(0)
        repeat task.wait() until not player:GetAttribute("LastACPos")
        player.Character.HumanoidRootPart.CFrame = CFrame.new(location.Position)
    end)

    if success then
        notify("Teleport", "Teleported to " .. location.Name, 3)
        task.delay(1.5, function()
            if screenGui then
                screenGui:Destroy()
            end
        end)
    else
        if screenGui then
            screenGui:Destroy()
        end
    end
end

for _, location in ipairs(TeleportLocations) do
    Section2:AddButton({
        Title = "Teleport to " .. location.Name,
        Callback = function()
            teleportToLocation(location)
        end
    })
end

local Section6 = Tabs.Exploits:AddSection("Safe Dupe")
Section6:AddButton({
    Title = "Infinite Money",
    Callback = function()
        local World = game.Workspace
        local Player = game.Players.LocalPlayer
        local Character = Player.Character
        local Humanoid = Character and Character:FindFirstChild("Humanoid")
        local HumanoidRootPart = Character and Character:FindFirstChild("HumanoidRootPart")

        local screenGui = Instance.new("ScreenGui")
        screenGui.Name = "TeleportOverlay"
        screenGui.ResetOnSpawn = false
        screenGui.Parent = game:GetService("CoreGui")

        local blackFrame = Instance.new("Frame")
        blackFrame.BackgroundColor3 = Color3.new(0, 0, 0)
        blackFrame.Size = UDim2.new(1, 0, 1, 0)
        blackFrame.BackgroundTransparency = 0
        blackFrame.BorderSizePixel = 0
        blackFrame.Parent = screenGui

        local function Teleport(Pos)
            if Humanoid and HumanoidRootPart then
                Humanoid:ChangeState(0)
                repeat task.wait() until not Player:GetAttribute("LastACPos")
                HumanoidRootPart.CFrame = CFrame.new(Pos)
            end
        end

        local character = Player.Character or Player.CharacterAdded:Wait()
        local hrp = character:WaitForChild("HumanoidRootPart")
        local oldCFrame = hrp.CFrame

        local function FindItem(Item)
            return Player.Backpack:FindFirstChild(Item) or Player.Character:FindFirstChild(Item)
        end

        local icefruitcupz = FindItem("Ice-Fruit Cupz")
        local SellPart = World:FindFirstChild("IceFruit Sell")
        local SellPrompt = SellPart and SellPart:FindFirstChild("ProximityPrompt")

        if not icefruitcupz then
            notify("Error", "You need Ice-Fruit Cupz to sell", 3)
            screenGui:Destroy()
            return
        end

        if not (SellPart and SellPrompt) then
            notify("Error", "Invalid sell point", 3)
            screenGui:Destroy()
            return
        end

        Humanoid:EquipTool(icefruitcupz)
        Teleport(SellPart.Position)
        task.wait(0.25)
        for _ = 1, 2000 do
            fireproximityprompt(SellPrompt)
        end

        notify("Success", "Done.", 3)
        Teleport(oldCFrame.Position)

        task.delay(1, function()
            if screenGui then
                screenGui:Destroy()
            end
        end)
    end
})

local lastDupeTime = 0
local dupeCooldown = 25

Section6:AddButton({
    Title = "Safe Dupe",
    Callback = function()
        local currentTime = os.time()
        if currentTime - lastDupeTime < dupeCooldown then
            notify("Cooldown", "Please wait " .. (dupeCooldown - (currentTime - lastDupeTime)) .. " seconds before duping again!", 3)
            return
        end

        lastDupeTime = currentTime

        local function v165()
            local player = game:GetService("Players").LocalPlayer
            local gui = player:FindFirstChild("PlayerGui")
            if not gui then return end

            local blackout = Instance.new("ScreenGui")
            blackout.Name = "TeleportBlackout"
            blackout.Parent = gui

            local frame = Instance.new("Frame")
            frame.Size = UDim2.new(1, 0, 1, 0)
            frame.Position = UDim2.new(0, 0, 0, 0)
            frame.BackgroundColor3 = Color3.new(0, 0, 0)
            frame.BackgroundTransparency = 0
            frame.Parent = blackout

            task.delay(2.5, function()
                if blackout then blackout:Destroy() end
            end)

            return blackout
        end

        v165()

        local replicatedStorage = game:GetService("ReplicatedStorage")
        local players = game:GetService("Players")
        local workspace = game:GetService("Workspace")

        local function getCharacter()
            return players.LocalPlayer.Character
        end

        local function teleportTo(position)
            game:GetService("Players").LocalPlayer.Character.Humanoid:ChangeState(0)
            repeat task.wait() until not game:GetService("Players").LocalPlayer:GetAttribute("LastACPos")
            game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(position.Position.X + 2, position.Position.Y, position.Position.Z)
        end

        local inventory = replicatedStorage:WaitForChild("Inventory")
        local backpackRemote = replicatedStorage:WaitForChild("BackpackRemote")

        if getCharacter():FindFirstChildOfClass("Tool") then
            local step = 0
            local toolName
            local safe
            local originalCFrame

            while true do
                if step == 4 then
                    task.wait(0.5)
                    teleportTo(originalCFrame)
                    notify("Safe Dupe", "Done", 5)
                    break
                end
                if step == 2 then
                    task.spawn(function()
                        backpackRemote:InvokeServer("Store", toolName)
                    end)
                    task.spawn(function()
                        inventory:FireServer("Change", toolName, "Backpack", safe)
                    end)
                    task.wait(1.5)
                    step = 3
                end
                if step == 3 then
                    teleportTo(originalCFrame)
                    task.wait(1)
                    backpackRemote:InvokeServer("Grab", toolName)
                    step = 4
                end
                if step == 0 then
                    toolName = getCharacter():FindFirstChildOfClass("Tool").Name
                    getCharacter():FindFirstChildOfClass("Humanoid"):UnequipTools()
                    safe = workspace["1# Map"]["2 Crosswalks"].Safes:GetChildren()[1]
                    step = 1
                end
                if step == 1 then
                    originalCFrame = getCharacter():FindFirstChild("HumanoidRootPart").CFrame
                    teleportTo(safe.Part.CFrame)
                    task.wait(0.5)
                    step = 2
                end
            end
        else
            notify('Safe Dupe', 'No Tool Found', 5)
        end
    end
})

local Section3 = Tabs.Exploits:AddSection("Exotic Dealer")

local ExoticItems = {
    { Name = "Ice Fruit Bag", Arg = "Ice-Fruit Bag" },
    { Name = "Ice Fruit Cupz", Arg = "Ice-Fruit Cupz" },
    { Name = "Fiji Water", Arg = "FijiWater" },
    { Name = "Fresh Water", Arg = "FreshWater" },
}

local function purchaseItem(itemName, itemArg)
    local args = { [1] = itemArg }
    local success = pcall(function()
        game:GetService("ReplicatedStorage"):WaitForChild("ExoticShopRemote"):InvokeServer(unpack(args))
    end)
    if success then
        notify("Exotic Dealer", "Purchased " .. itemName .. "!", 3)
    else
        notify("Exotic Dealer", "Failed to purchase " .. itemName .. "!", 3)
    end
end

for _, item in ipairs(ExoticItems) do
    Section3:AddButton({
        Title = "Buy " .. item.Name,
        Callback = function()
            purchaseItem(item.Name, item.Arg)
        end
    })
end

local Section4 = Tabs.Exploits:AddSection("Quick Buy")

local QuickBuyItems = {
    { Name = "Shiesty", Arg = "Shiesty" },
    { Name = "Blue Gloves", Arg = "BluGloves" },
    { Name = "White Gloves", Arg = "WhiteGloves" },
    { Name = "Black Gloves", Arg = "BlackGloves" },
    { Name = "Water", Arg = "Water" },
}

local function purchaseItemQ(itemName, itemArg)
    local success, response = pcall(function()
        return game:GetService("ReplicatedStorage").ShopRemote:InvokeServer(itemArg)
    end)
    
    if success then
        notify("Quick Purchase", itemName .. " purchased!", 3)
    else
        notify("Quick Purchase", "Couldn't buy " .. itemName .. ": " .. tostring(response), 5)
    end
end

for _, item in ipairs(QuickBuyItems) do
    Section4:AddButton({
        Title = "Buy " .. item.Name,
        Callback = function()
            purchaseItemQ(item.Name, item.Arg)
        end
    })
end

local Section5 = Tabs.Home:AddSection("Bypasses")

local function instantPrompts()
    for _, v in ipairs(game:GetService("Workspace"):GetDescendants()) do
        if v:IsA("ProximityPrompt") then
            v.HoldDuration = 0
        end
    end
    
    game:GetService("Workspace").DescendantAdded:Connect(function(v)
        if v:IsA("ProximityPrompt") then
            v.HoldDuration = 0
        end
    end)
end

local function antiFall()
    local function checkFallDamage()
        local player = game.Players.LocalPlayer
        if player and player.Character then
            local fallDamage = player.Character:FindFirstChild("FallDamageRagdoll")
            if fallDamage then
                fallDamage.Disabled = true
            end
        end
    end
    

    checkFallDamage()
end

local function antiHunger()
    local function disableHunger()
        local player = game.Players.LocalPlayer
        if not player or not player:FindFirstChild("PlayerGui") then return end

        for _, descendant in ipairs(player.PlayerGui:GetDescendants()) do
            if descendant:IsA("NumberValue") or descendant:IsA("IntValue") then
                if string.lower(descendant.Name):find("hunger") then
                    descendant.Value = 100
                end
            end
            if (descendant:IsA("LocalScript") or descendant:IsA("Script")) and string.lower(descendant.Name):find("hunger") then
                descendant.Disabled = true
            end
        end
    end

    disableHunger()
end

local function antiSleep()
    local function disableSleep()
        local player = game.Players.LocalPlayer
        if player and player:FindFirstChild("PlayerGui") then
            local sleepGui = player.PlayerGui:FindFirstChild("SleepGui")
            if sleepGui then
                local sleepScript = sleepGui:FindFirstChild("Frame") and sleepGui.Frame:FindFirstChild("sleep") and sleepGui.Frame.sleep:FindFirstChild("SleepBar") and sleepGui.Frame.sleep.SleepBar:FindFirstChild("sleepScript")
                if sleepScript then
                    sleepScript.Disabled = true
                end
            end
        end
    end
    
    disableSleep()
end

local function antiStamina()
    local player = game.Players.LocalPlayer
    if not player or not player:FindFirstChild("PlayerGui") then return end

    local function setStaminaToFull(obj)
        if (obj:IsA("NumberValue") or obj:IsA("IntValue")) and string.find(string.lower(obj.Name), "stamina") then
            obj.Value = 100
        end
    end

    local function disableAndSetStamina(parent)
        for _, child in pairs(parent:GetChildren()) do
            if child:IsA("LocalScript") or child:IsA("Script") or child:IsA("ModuleScript") then
                if string.find(string.lower(child.Name), "stamina") then
                    child.Disabled = true
                end
            end

            setStaminaToFull(child)

            disableAndSetStamina(child)
        end
    end

    disableAndSetStamina(player.PlayerGui)
end

local function antiCameraShake()
    local function removeCameraBobbing()
        local player = game.Players.LocalPlayer
        if player and player.Character then
            local cameraBobbing = player.Character:FindFirstChild("CameraBobbing")
            if cameraBobbing then
                cameraBobbing:Destroy()
            end
        end
    end
    
    removeCameraBobbing()
end

local function antiRentPay()
    local player = game:GetService("Players").LocalPlayer
    local rentGui = player:FindFirstChild("PlayerGui") and player.PlayerGui:FindFirstChild("RentGui")
    
    if rentGui then
        local rentScript = rentGui:FindFirstChild("LocalScript")
        if rentScript then
            rentScript.Disabled = true
            rentScript:Destroy()
        end
    end
end

local function antiKnockback()
    for _, v in ipairs(game.Players.LocalPlayer.Character:GetDescendants()) do
        if (v:IsA("BodyVelocity") or v:IsA("LinearVelocity") or v:IsA("VectorForce")) then
            v:Destroy()
        end
    end
    
    if game.ReplicatedStorage:FindFirstChild("AE") then
        game.ReplicatedStorage.AE:Destroy()
    end
    
    game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart").ChildAdded:Connect(function(v)
        if (v:IsA("BodyVelocity") or v:IsA("LinearVelocity") or v:IsA("VectorForce")) then
            v:Destroy()
        end
    end)
end

local function antiJumpCooldown()
    local player = game:GetService("Players").LocalPlayer
    local playerGui = player:FindFirstChild("PlayerGui")
    
    if playerGui then
        local jumpDebounce = playerGui:FindFirstChild("JumpDebounce")
        if jumpDebounce then
            jumpDebounce:Destroy()
        end
    end
end

Section5:AddButton({
    Title = "Instant Prompts",
    Callback = function()
        instantPrompts()
    end
})

Section5:AddButton({
    Title = "Anti-Fall Damage",
    Callback = function()
        antiFall()
    end
})

Section5:AddButton({
    Title = "Anti Hunger",
    Callback = function()
        antiHunger()
    end
})

Section5:AddButton({
    Title = "Anti Sleep",
    Callback = function()
        antiSleep()
    end
})

Section5:AddButton({
    Title = "No Stamina Drain",
    Callback = function()
        antiStamina()
    end
})

Section5:AddButton({
    Title = "Anti-CameraShake",
    Callback = function()
        antiCameraShake()
    end
})

Section5:AddButton({
    Title = "Anti-RentPay",
    Callback = function()
        antiRentPay()
    end
})

Section5:AddButton({
    Title = "Anti-Knockback",
    Callback = function()
        antiKnockback()
    end
})

Section5:AddButton({
    Title = "Anti-JumpCooldown",
    Callback = function()
        antiJumpCooldown()
    end
})

local BankSection = Tabs.Bank:AddSection("Bank")

local atmbankamount = nil
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local BankAction = ReplicatedStorage:WaitForChild("BankAction")
local BankProcessRemote = ReplicatedStorage:WaitForChild("BankProcessRemote")

local cashInput = BankSection:AddInput("CashAmount", {
    Title = "Cash Amount",
    Placeholder = "Enter cash amount",
    Numeric = true,
    Default = "",
    Finished = true,
    Callback = function(text)
        local amount = tonumber(text)
        if amount and amount > 0 then
            atmbankamount = amount
        else
            atmbankamount = nil
        end
    end
})

local function sendBankRequest(action)
    if not atmbankamount then
        notify("Bank", "Invalid cash amount. Please enter a positive number.", 5)
        return
    end

    if action == "Drop" then
        local success, err = pcall(function()
            BankProcessRemote:InvokeServer(action, atmbankamount)
        end)
        if success then
            notify("Drop", "Cash dropped successfully.")
        else
            notify("Drop", "Error dropping cash: " .. tostring(err), 5)
        end
    else
        BankAction:FireServer(action, atmbankamount)
        notify(action == "depo" and "Deposited " or "Withdrew " .. atmbankamount .. " cash.")
    end
end

BankSection:AddButton({
    Title = "Deposit",
    Callback = function()
        sendBankRequest("depo")
    end
})

BankSection:AddButton({
    Title = "Withdraw",
    Callback = function()
        sendBankRequest("with")
    end
})

BankSection:AddButton({
    Title = "Drop",
    Callback = function()
        sendBankRequest("Drop")
    end
})

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local SectionC = Tabs.Combat:AddSection("Hitbox")

local enabled = false
local size = 2
local transparency = 0.8

local function applyHitbox()
	for _, player in ipairs(Players:GetPlayers()) do
		if player ~= LocalPlayer and player ~= currentTarget and player.Character and player.Character:FindFirstChild("Head") then
			local head = player.Character.Head
			head.Size = Vector3.new(size, size, size)
			head.Transparency = transparency
			head.Material = Enum.Material.Neon
			head.BrickColor = BrickColor.Red()
			head.CanCollide = false
		end
	end
end

SectionC:AddSlider("HSize", {Title = "Hitbox Size", Default = 7, Min = 1, Max = 15, Rounding = 1}):OnChanged(function(val)
    size = val
	if enabled then applyHitbox() end
end)

SectionC:AddToggle("HitboxExpander", { Title = "Hitbox Expander", Default = false }):OnChanged(function()
    enabled = Options.HitboxExpander.Value
    if enabled then
        task.spawn(function()
            while enabled do
                applyHitbox()
                task.wait(0.1)
            end
        end)
    else
        for _, player in ipairs(Players:GetPlayers()) do
            if player ~= LocalPlayer and player ~= currentTarget and player.Character and player.Character:FindFirstChild("Head") then
                local head = player.Character.Head
                head.Size = Vector3.new(2, 1, 1)
                head.Transparency = 0
                head.Material = Enum.Material.Plastic
                head.BrickColor = BrickColor.new("Medium stone grey")
            end
        end
    end
end)

local Players = game:GetService("Players")
local Camera = workspace.CurrentCamera
local LocalPlayer = Players.LocalPlayer

local currentTarget = nil

local function updateDropdown()
	local names = {}
	for _, player in ipairs(Players:GetPlayers()) do
		if player ~= LocalPlayer then
			table.insert(names, player.Name)
		end
	end
	return names
end

local ESPESection = Tabs.Visual:AddSection("Spectate")

local Dropdown = ESPESection:AddDropdown("Dropdown", {
    Title = "Player",
    Values = updateDropdown(),
    Multi = false,
    Default = 0,
})

Dropdown:OnChanged(function(Value)
    enabled = false
    local target = Players:FindFirstChild(Value)
	if target and target.Character and target.Character:FindFirstChild("Humanoid") then
		Camera.CameraSubject = target.Character.Humanoid
		Camera.CameraType = Enum.CameraType.Custom
		currentTarget = target
	end
end)

ESPESection:AddButton({
    Title = "Unspectate",
    Callback = function()
        Camera.CameraSubject = LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") or LocalPlayer
	    currentTarget = nil
        enabled = true
    end
})

local ESPSection = Tabs.Visual:AddSection("ESP")

local ESP_SETTINGS = {
    Name = false,
    Health = false,
    Distance = false,
    Highlight = false,
    Holding = false,
    Tracers = false,
    Box = false,
    HealthBar = false,
    TracerPosition = "Bottom"
}

local function getHeldItem(character)
    if character then
        for _, tool in pairs(character:GetChildren()) do
            if tool:IsA("Tool") then
                return tool.Name
            end
        end
    end
    return nil
end

local function createESP(player)
    if player == game.Players.LocalPlayer then return end
    
    local function setupCharacter(character)
        if not character then return end
        
        local head = character:FindFirstChild("Head")
        local humanoid = character:FindFirstChildOfClass("Humanoid")
        local rootPart = character:FindFirstChild("HumanoidRootPart")
        if not head or not humanoid or not rootPart then return end
        
        for _, child in pairs(character:GetChildren()) do
            if child:IsA("BillboardGui") or child:IsA("Highlight") then
                child:Destroy()
            end
        end

        local nameGui = Instance.new("BillboardGui")
        nameGui.Name = "PlayerESP"
        nameGui.Parent = head
        nameGui.Adornee = head
        nameGui.Size = UDim2.new(5, 0, 1, 0)
        nameGui.StudsOffset = Vector3.new(0, 3, 0)
        nameGui.AlwaysOnTop = true

        local nameLabel = Instance.new("TextLabel")
        nameLabel.Parent = nameGui
        nameLabel.Size = UDim2.new(1, 0, 1, 0)
        nameLabel.BackgroundTransparency = 1
        nameLabel.TextSize = 15
        nameLabel.TextColor3 = Color3.new(1, 1, 1)
        nameLabel.Font = Enum.Font.Gotham
        nameLabel.TextStrokeTransparency = 0
        nameLabel.TextStrokeColor3 = Color3.new(0, 0, 0)
        nameLabel.RichText = true

        local distanceGui = Instance.new("BillboardGui")
        distanceGui.Name = "DistanceHoldingESP"
        distanceGui.Parent = rootPart
        distanceGui.Adornee = rootPart
        distanceGui.Size = UDim2.new(4, 0, 0.2, 0)
        distanceGui.StudsOffset = Vector3.new(0, -2.5, 0)
        distanceGui.AlwaysOnTop = true

        local distanceLabel = Instance.new("TextLabel")
        distanceLabel.Parent = distanceGui
        distanceLabel.Size = UDim2.new(1, 0, 1, 0)
        distanceLabel.BackgroundTransparency = 1
        distanceLabel.TextSize = 15
        distanceLabel.TextColor3 = Color3.new(1, 1, 1)
        distanceLabel.Font = Enum.Font.Gotham
        distanceLabel.TextStrokeTransparency = 0
        distanceLabel.TextStrokeColor3 = Color3.new(0, 0, 0)

        local highlight = Instance.new("Highlight")
        highlight.Parent = character
        highlight.Name = "HighlightESP"
        highlight.FillColor = Color3.fromRGB(255, 255, 255)
        highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
        highlight.FillTransparency = 0.5
        highlight.OutlineTransparency = 0.2

        local box = Instance.new("BoxHandleAdornment")
        box.Name = "BoxESP"
        box.Parent = rootPart
        box.Adornee = rootPart
        box.Size = Vector3.new(2, 3, 1)
        box.Transparency = 0.7
        box.Color3 = Color3.new(1, 1, 1)
        box.AlwaysOnTop = true

        local healthBar = Instance.new("BillboardGui")
        healthBar.Name = "HealthBarESP"
        healthBar.Parent = rootPart
        healthBar.Adornee = rootPart
        healthBar.Size = UDim2.new(2, 0, 0.2, 0)
        healthBar.StudsOffset = Vector3.new(0, -3, 0)
        healthBar.AlwaysOnTop = true

        local healthBarFrame = Instance.new("Frame")
        healthBarFrame.Parent = healthBar
        healthBarFrame.Size = UDim2.new(1, 0, 0.3, 0)
        healthBarFrame.BackgroundColor3 = Color3.new(0, 0, 0)
        healthBarFrame.BorderSizePixel = 1

        local healthBarFill = Instance.new("Frame")
        healthBarFill.Parent = healthBarFrame
        healthBarFill.Size = UDim2.new(1, 0, 1, 0)
        healthBarFill.BackgroundColor3 = Color3.new(0, 1, 0)
        healthBarFill.BorderSizePixel = 0

        local tracer = Drawing.new("Line")
        tracer.Visible = false
        tracer.Color = Color3.new(1, 1, 1)
        tracer.Thickness = 1
        tracer.Transparency = 1

        local connection
        connection = game:GetService("RunService").Heartbeat:Connect(function()
            if not character or not rootPart then 
                if connection then connection:Disconnect() end
                if tracer then tracer:Remove() end
                return 
            end
            
            if humanoid then
                local healthPercent = math.floor((humanoid.Health / humanoid.MaxHealth) * 100)
                local healthColor = Color3.new(1 - healthPercent/100, healthPercent/100, 0)
                
                local nameText = ESP_SETTINGS.Name and player.Name or ""
                local healthText = ESP_SETTINGS.Health and ("HP: "..healthPercent.."%") or ""
                local separator = (ESP_SETTINGS.Name and ESP_SETTINGS.Health) and " | " or ""
                
                nameLabel.Text = nameText .. separator .. healthText
                nameGui.Enabled = ESP_SETTINGS.Name or ESP_SETTINGS.Health
                nameLabel.Visible = ESP_SETTINGS.Name or ESP_SETTINGS.Health

                local distanceText = ESP_SETTINGS.Distance and ("["..math.floor((game.Players.LocalPlayer.Character.HumanoidRootPart.Position - rootPart.Position).Magnitude).."m]") or ""
                local heldItem = ESP_SETTINGS.Holding and getHeldItem(character)
                local holdingText = heldItem and ("["..heldItem.."]") or ""
                
                distanceLabel.Text = distanceText .. " " .. holdingText
                distanceGui.Enabled = ESP_SETTINGS.Distance or ESP_SETTINGS.Holding

                highlight.Enabled = ESP_SETTINGS.Highlight
                box.Visible = ESP_SETTINGS.Box
                healthBar.Enabled = ESP_SETTINGS.HealthBar
                healthBarFill.Size = UDim2.new(humanoid.Health/humanoid.MaxHealth, 0, 1, 0)
                healthBarFill.BackgroundColor3 = healthColor

                if ESP_SETTINGS.Tracers then
                    local vector, onScreen = workspace.CurrentCamera:WorldToViewportPoint(rootPart.Position)
                    if onScreen then
                        if ESP_SETTINGS.TracerPosition == "Top" then
                            tracer.From = Vector2.new(workspace.CurrentCamera.ViewportSize.X/2, 0)
                        else
                            tracer.From = Vector2.new(workspace.CurrentCamera.ViewportSize.X/2, workspace.CurrentCamera.ViewportSize.Y)
                        end
                        tracer.To = Vector2.new(vector.X, vector.Y)
                        tracer.Visible = true
                    else
                        tracer.Visible = false
                    end
                else
                    tracer.Visible = false
                end
            end
        end)

        character.AncestryChanged:Connect(function()
            if not character:IsDescendantOf(workspace) then
                if connection then connection:Disconnect() end
                if tracer then tracer:Remove() end
            end
        end)
    end

    if player.Character then
        setupCharacter(player.Character)
    end

    player.CharacterAdded:Connect(function(character)
        task.wait(1)
        setupCharacter(character)
    end)
end

local function toggleESP(value)
    if value then
        for _, player in pairs(game:GetService("Players"):GetPlayers()) do
            createESP(player)
        end
        
        game:GetService("Players").PlayerAdded:Connect(function(player)
            createESP(player)
        end)
    else
        for _, player in pairs(game:GetService("Players"):GetPlayers()) do
            if player.Character then
                for _, child in pairs(player.Character:GetDescendants()) do
                    if child.Name == "PlayerESP" or child.Name == "DistanceHoldingESP" or 
                       child.Name == "HighlightESP" or child.Name == "BoxESP" or 
                       child.Name == "HealthBarESP" then
                        child:Destroy()
                    end
                end
            end
        end
    end
end

ESPSection:AddToggle("ESPNameToggle", { Title = "Name", Default = false }):OnChanged(function()
    ESP_SETTINGS.Name = Options.ESPNameToggle.Value
    toggleESP(Options.ESPNameToggle.Value or ESP_SETTINGS.Health or ESP_SETTINGS.Distance or 
             ESP_SETTINGS.Highlight or ESP_SETTINGS.Holding or ESP_SETTINGS.Tracers or 
             ESP_SETTINGS.Box or ESP_SETTINGS.HealthBar)
end)

ESPSection:AddToggle("ESPHealthToggle", { Title = "Health", Default = false }):OnChanged(function()
    ESP_SETTINGS.Health = Options.ESPHealthToggle.Value
    toggleESP(Options.ESPHealthToggle.Value or ESP_SETTINGS.Name or ESP_SETTINGS.Distance or 
             ESP_SETTINGS.Highlight or ESP_SETTINGS.Holding or ESP_SETTINGS.Tracers or 
             ESP_SETTINGS.Box or ESP_SETTINGS.HealthBar)
end)

ESPSection:AddToggle("ESPDistanceToggle", { Title = "Distance", Default = false }):OnChanged(function()
    ESP_SETTINGS.Distance = Options.ESPDistanceToggle.Value
    toggleESP(Options.ESPDistanceToggle.Value or ESP_SETTINGS.Name or ESP_SETTINGS.Health or 
             ESP_SETTINGS.Highlight or ESP_SETTINGS.Holding or ESP_SETTINGS.Tracers or 
             ESP_SETTINGS.Box or ESP_SETTINGS.HealthBar)
end)

ESPSection:AddToggle("ESPHighlightToggle", { Title = "Highlight", Default = false }):OnChanged(function()
    ESP_SETTINGS.Highlight = Options.ESPHighlightToggle.Value
    toggleESP(Options.ESPHighlightToggle.Value or ESP_SETTINGS.Name or ESP_SETTINGS.Health or 
             ESP_SETTINGS.Distance or ESP_SETTINGS.Holding or ESP_SETTINGS.Tracers or 
             ESP_SETTINGS.Box or ESP_SETTINGS.HealthBar)
end)

ESPSection:AddToggle("ESPHoldingToggle", { Title = "Holding", Default = false }):OnChanged(function()
    ESP_SETTINGS.Holding = Options.ESPHoldingToggle.Value
    toggleESP(Options.ESPHoldingToggle.Value or ESP_SETTINGS.Name or ESP_SETTINGS.Health or 
             ESP_SETTINGS.Distance or ESP_SETTINGS.Highlight or ESP_SETTINGS.Tracers or 
             ESP_SETTINGS.Box or ESP_SETTINGS.HealthBar)
end)

ESPSection:AddToggle("ESPTracersToggle", { Title = "Tracers", Default = false }):OnChanged(function()
    ESP_SETTINGS.Tracers = Options.ESPTracersToggle.Value
    toggleESP(Options.ESPTracersToggle.Value or ESP_SETTINGS.Name or ESP_SETTINGS.Health or 
             ESP_SETTINGS.Distance or ESP_SETTINGS.Highlight or ESP_SETTINGS.Holding or 
             ESP_SETTINGS.Box or ESP_SETTINGS.HealthBar)
end)

ESPSection:AddDropdown("TracerPosition", { Title = "Tracer Position", Values = {"Top", "Bottom"}, Default = "Bottom" }):OnChanged(function(value)
    ESP_SETTINGS.TracerPosition = value
end)

ESPSection:AddToggle("ESPHealthBarToggle", { Title = "Health Bar", Default = false }):OnChanged(function()
    ESP_SETTINGS.HealthBar = Options.ESPHealthBarToggle.Value
    toggleESP(Options.ESPHealthBarToggle.Value or ESP_SETTINGS.Name or ESP_SETTINGS.Health or 
             ESP_SETTINGS.Distance or ESP_SETTINGS.Highlight or ESP_SETTINGS.Tracers or 
             ESP_SETTINGS.Box)
end)

SaveManager:SetLibrary(Fluent)
InterfaceManager:SetLibrary(Fluent)
SaveManager:IgnoreThemeSettings()
SaveManager:SetIgnoreIndexes({})
InterfaceManager:SetFolder("Sensational")
SaveManager:SetFolder("Sensational/bronx")
InterfaceManager:BuildInterfaceSection(Tabs.Settings)
SaveManager:BuildConfigSection(Tabs.Settings)
Window:SelectTab(1)
SaveManager:LoadAutoloadConfig()
