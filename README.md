local Rayfield = loadstring(game:HttpGet('https://raw.githubusercontent.com/shlexware/Rayfield/main/source'))()

local Window = Rayfield:CreateWindow({
	Name = "X HUB",
	LoadingTitle = "X HUB",
	LoadingSubtitle = "X HUB",
	ConfigurationSaving = {
		Enabled = false,
		FolderName = "X HUB",
		FileName = "X Hub"
	},
	KeySystem = true,
	KeySettings = {
		Title = "X Hub",
		Subtitle = "Key",
		Note = "Ket = x",
		SaveKey = false,
		Key = "x"
	}
})

Rayfield:Notify("Title Example", "Content/Description Example", 4483362458)

local Tab = Window:CreateTab("Tab Example", 4483362458) 

local Section = Tab:CreateSection("เลือกอาวุธ")

Wapon = {}
for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
    if v:IsA("Tool") then
       table.insert(Wapon ,v.Name)
    end
end
for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do  
    if v:IsA("Tool") then
       table.insert(Wapon, v.Name)
    end
end

MonName = {

  "Bandit Lv1",
  "Bandit Boss Lv50",
  "Monkey Lv100",
  "Golila Lv200",
  "Bandit sand Lv300",
  "bandit sand Lv400",
  "Sokamona Lv???/",
  "Monkey King Lv???",
  "Sword man Lv???",
  "blackman Lv???"
}

local Dropdown = Tab:CreateDropdown({
	Name = "อาวุธ",
	Options = Wapon,
	CurrentOption = "",
	Flag = "Dropdown1",
	Callback = function(Value)
	  		_G.Weapon = Value
	end,
})

local Button = Tab:CreateButton({
	Name = "รีเช็ตอาวุธ",
	Callback = function()
Wapon = {}
        for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
    if v:IsA("Tool") then
       table.insert(Wapon ,v.Name)
    end
end
for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do  
    if v:IsA("Tool") then
       table.insert(Wapon, v.Name)
    end
end
              Weapon_Tab:Refresh(Wapon,true)
      end,    
})

local Section = Tab:CreateSection("เลือกมอน")

local Dropdown = Tab:CreateDropdown({
	Name = "เลือกมอน",
	Options = MonName,
	CurrentOption = "",
	Flag = "Dropdown1",
	Callback = function(Value)
	  	_G.Monster = Value
	end,
})



function TP(CFrame)
    pcall(function()
        game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart").CFrame = CFrame
    end)
end


function EquipWeapon(ToolSe)
		if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
			Tool = game.Players.LocalPlayer.Backpack:WaitForChild(ToolSe)
			wait(.1)
			game.Players.LocalPlayer.Character.Humanoid:EquipTool(Tool)
	end
end



local Toggle = Tab:CreateToggle({
	Name = "ฟามมอน",
	CurrentValue = false,
	Flag = "Toggle1",
	Callback = function(Value)
		  pcall(function()
		_G.Auto_Farm_Monster = true
        _G.NOCLIP = Value
if Value then
    AutoFarmMonster()
    else
        _G.Auto_Farm_Monster = false
        NoclipToFly:Destroy()
       game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip"):Destroy()
          end
     end)
	end,
})


spawn(function()
    pcall(function()
        game:GetService("RunService").Heartbeat:Connect(function()
            if _G.NOCLIPRanbow then
                if not game:GetService("Workspace"):FindFirstChild("LOL") then
                    Paertaiteen = Instance.new("Part")
                    Paertaiteen.Name = "LOL"
                    Paertaiteen.Parent = game.Workspace
                    Paertaiteen.Anchored = true
                    Paertaiteen.Transparency = 1
                    Paertaiteen.Size = Vector3.new(15,0.5,15)
                    Paertaiteen.Material = "Neon"
                elseif game:GetService("Workspace"):FindFirstChild("LOL") then
                    pcall(function()
                    game.Workspace["LOL"].CFrame = CFrame.new(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.X,game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.Y - 3.92,game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.Z)
                    end)
                end
            else
                if game:GetService("Workspace"):FindFirstChild("LOL") then
                    game:GetService("Workspace"):FindFirstChild("LOL"):Destroy()
                end
            end
        end)
    end)
 end)

function AutoFarmMonster()

    spawn(function()

        while _G.Auto_Farm_Monster == true do wait()
            pcall(function()
                if not game:GetService("Players").LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") and _G.Auto_Farm_Monster == true then
                    NoclipToFly = Instance.new("BodyVelocity")
                    NoclipToFly.Name = "BodyClip"
                    NoclipToFly.Parent = game:GetService("Players").LocalPlayer.Character.HumanoidRootPart
                    NoclipToFly.MaxForce = Vector3.new(100000,100000,100000)
                    NoclipToFly.Velocity = Vector3.new(0,0,0)
                elseif _G.Auto_Farm_Monster == false then
                    NoclipToFly:Destroy()
                end
                EquipWeapon(tostring(_G.Weapon))
            for i,v in pairs(game:GetService("Workspace")["Map[All]"]:GetDescendants()) do
                if v:FindFirstChild("Humanoid") and v.Name ~= game.Players.LocalPlayer.Name  then
                    v.Humanoid:ChangeState(11)
                    v.Humanoid:ChangeState(14)
                    v.HumanoidRootPart.Size = Vector3.new(60,60,60)
                    v.HumanoidRootPart.Transparency = 1
            if v.Name == tostring(_G.Monster) and v.Humanoid.Health >0 and v.Name ~= " " and v.Name ~= "" then
                chosenDemon = false
                if chosenDemon == false then
				TP(v.HumanoidRootPart.CFrame * CFrame.new(0,-4,5))
game.Players.LocalPlayer.Character[_G.Weapon]:Activate()
                v.Humanoid.HealthChanged:Connect(function()
                    if v.Humanoid.Health <= 0 then
                        chosenDemon = true
                               end
                          end)
                     end
                end
           end
      end
end)
      end
           end)
                 end


spawn(function()
	pcall(function()
		game:GetService("RunService").Stepped:Connect(function()
			if _G.NOCLIP == true then
				for i,v in pairs(game:GetService("Players").LocalPlayer.Character:GetDescendants()) do
					if v:IsA("BasePart") then
						v.CanCollide = false    
					end
				end
			end
		end)
	end)
end)
