local CoreGui = game.Players.LocalPlayer:WaitForChild("PlayerGui")
local TweenService = game:GetService("TweenService")

local TweenScrollInfo = TweenInfo.new(0.1, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)
local TweenTabInfo = TweenInfo.new(0.25, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)

local NotifyTweenInfo = TweenInfo.new(.45, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
local NotifyCatchUpInfo = TweenInfo.new(0.3, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)

local TweenColorToggleInfo = TweenInfo.new(0.2, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)

local TweenDropDownInfo = TweenInfo.new(0.3, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)

local BasicLibrary = {}

local NotificationsList = nil

local function CreateNewDropdownButton(String, Parent)
	local Button = Instance.new("Frame")
	local UIListLayout = Instance.new("UIListLayout")
	local TextButton = Instance.new("TextButton")
	
	Button.Name = "Button"
	Button.Parent = Parent
	Button.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Button.BackgroundTransparency = 1.000
	Button.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Button.BorderSizePixel = 0
	Button.Position = UDim2.new(0, 0, -0.150000006, 0)
	Button.Size = UDim2.new(1, 0, 0.717948735, 0)

	UIListLayout.Parent = Button
	UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
	UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
	UIListLayout.VerticalAlignment = Enum.VerticalAlignment.Center

	TextButton.Parent = Button
	TextButton.BackgroundColor3 = Color3.fromRGB(85, 170, 255)
	TextButton.BackgroundTransparency = 1.000
	TextButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
	TextButton.BorderSizePixel = 0
	TextButton.Position = UDim2.new(0.053418804, 0, 0.296037167, 0)
	TextButton.Size = UDim2.new(0.919, 0, 0.679, 0)
	TextButton.Font = Enum.Font.SourceSans
	TextButton.TextColor3 = Color3.fromRGB(255, 255, 255)
	TextButton.TextScaled = true
	TextButton.TextSize = 14.000
	TextButton.TextWrapped = true
	
	TextButton.Text = String
	
	return TextButton
end

local function CreateList()
	local ScreenGui = Instance.new("ScreenGui")
	
	local Frame = Instance.new("Frame")
	local UIListLayout = Instance.new("UIListLayout")

	ScreenGui.Parent = CoreGui
	ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

	Frame.Parent = ScreenGui
	Frame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Frame.BackgroundTransparency = 1.000
	Frame.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Frame.BorderSizePixel = 0
	Frame.Position = UDim2.new(0.729341328, 0, 0, 0)
	Frame.Size = UDim2.new(0.270658672, 0, 0.979655921, 0)

	UIListLayout.Parent = Frame
	UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
	UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
	UIListLayout.VerticalAlignment = Enum.VerticalAlignment.Bottom
	UIListLayout.Padding = UDim.new(0, 10)
	
	NotificationsList = Frame
end

local function FixDecimals(number)
	local numberStr = tostring(number)
	local decimalPosition = string.find(numberStr, ".", 1, true)
	local wholenumber = nil
	
	if decimalPosition then
		wholenumber = string.sub(numberStr, 1, decimalPosition - 1)
	else
		return number
	end
	
	local result = string.sub(numberStr, decimalPosition + 1)
	
	if tonumber(result) == 0 or decimalPosition == nil then return tonumber(number) end
	
	local StringsToRemove = 0
	
	for i = #result, 1, -1 do
		local char = string.sub(result, i, i)
		if tonumber(char) ~= nil and tonumber(char) == 0 then
			StringsToRemove = StringsToRemove+1
		elseif tonumber(char) ~= nil and tonumber(char) ~= 0 then
			break
		end
	end
	
	result = tonumber(wholenumber.."."..(string.sub(result, 1, #result - StringsToRemove)))
	
	return result
end

function BasicLibrary:New(Title)
	local ScreenGui = Instance.new("ScreenGui")
	local Drag = Instance.new("Frame")
	local Frame = Instance.new("Frame")
	local Frame_2 = Instance.new("Frame")
	local ScrollingFrame_Buttons = Instance.new("ScrollingFrame")
	local UIListLayout = Instance.new("UIListLayout")
	local TextLabel = Instance.new("TextLabel")

	ScreenGui.Parent = CoreGui
	ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

	Drag.Name = "Drag"
	Drag.Parent = ScreenGui
	Drag.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	Drag.BackgroundTransparency = 1.000
	Drag.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Drag.BorderSizePixel = 0
	Drag.Position = UDim2.new(0.270658672, 0, 0.257085025, 0)
	Drag.Size = UDim2.new(0.458682626, 0, 0.0384615399, 0)

	Frame.Parent = Drag
	Frame.BackgroundColor3 = Color3.fromRGB(37, 44, 57)
	Frame.BackgroundTransparency = 0.2
	Frame.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Frame.BorderSizePixel = 0
	Frame.Position = UDim2.new(3.98401809e-08, 0, 0.421052635, 0)
	Frame.Size = UDim2.new(0.99999994, 0, 11.7368355, 0)

	Frame_2.Parent = Frame
	Frame_2.BackgroundColor3 = Color3.fromRGB(20, 23, 30)
	Frame_2.BorderColor3 = Color3.fromRGB(0, 0, 0)
	Frame_2.BorderSizePixel = 0
	Frame_2.ClipsDescendants = true
	Frame_2.Position = UDim2.new(0.305483043, 0, 0.0493273549, 0)
	Frame_2.Size = UDim2.new(0.665796399, 0, 0.896861494, 0)

	ScrollingFrame_Buttons.Parent = Frame
	ScrollingFrame_Buttons.Active = true
	ScrollingFrame_Buttons.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	ScrollingFrame_Buttons.BackgroundTransparency = 1.000
	ScrollingFrame_Buttons.BorderColor3 = Color3.fromRGB(0, 0, 0)
	ScrollingFrame_Buttons.BorderSizePixel = 0
	ScrollingFrame_Buttons.Position = UDim2.new(0.0281733815, 0, 0.228536159, 0)
	ScrollingFrame_Buttons.Size = UDim2.new(0.261096627, 0, 0.717489183, 0)
	ScrollingFrame_Buttons.AutomaticCanvasSize = Enum.AutomaticSize.Y
	ScrollingFrame_Buttons.CanvasSize = UDim2.new(0, 0, 0, 0)

	UIListLayout.Parent = ScrollingFrame_Buttons
	UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
	UIListLayout.Padding = UDim.new(0, 10)

	TextLabel.Parent = Frame
	if Title == nil or tostring(Title) == nil then
		TextLabel.Text = "No title was set."
	else
		TextLabel.Text = Title
	end
	TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
	TextLabel.BackgroundTransparency = 1.000
	TextLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
	TextLabel.BorderSizePixel = 0
	TextLabel.Position = UDim2.new(0.0281733815, 0, 0.0493273549, 0)
	TextLabel.Size = UDim2.new(0.229765028, 0, 0.0717489198, 0)
	TextLabel.Font = Enum.Font.Code
	TextLabel.TextColor3 = Color3.fromRGB(235, 244, 255)
	TextLabel.TextScaled = true
	TextLabel.TextSize = 14.000
	TextLabel.TextWrapped = true

	--// Dragging

	local ______ = game:GetService("TweenService")
	local _________ = game:GetService("UserInputService")
	local dragging
	local dragInput
	local dragStart
	local startPos

	local function update(input)
		local delta = input.Position - dragStart
		local dragTime = 0.04
		local SmoothDrag = {}
		SmoothDrag.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
		local dragSmoothFunction = ______:Create(Drag, TweenInfo.new(dragTime, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), SmoothDrag)
		dragSmoothFunction:Play()
	end
	Drag.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			dragging = true
			dragStart = input.Position
			startPos = Drag.Position
			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
				end
			end)
		end
	end)
	Drag.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
		end
	end)
	_________.InputChanged:Connect(function(input)
		if input == dragInput and dragging and Drag.Size then
			update(input)
		end
	end)

	--// End of Dragging

	local UI = {}
	local TabSystem = {
		["CurrentTab"] = {0, nil, nil, nil, nil},
		["Buttons"] = {},
		["Tabs"] = {}
	}

	local function NewTab()
		local ScrollingFrame = Instance.new("ScrollingFrame")
		local UIListLayout = Instance.new("UIListLayout")
		
		ScrollingFrame.Parent = Frame_2
		ScrollingFrame.Visible = false
		ScrollingFrame.Active = true
		ScrollingFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
		ScrollingFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		ScrollingFrame.BackgroundTransparency = 1.000
		ScrollingFrame.BorderColor3 = Color3.fromRGB(0, 0, 0)
		ScrollingFrame.BorderSizePixel = 0
		ScrollingFrame.Size = UDim2.new(1, 0, 1, 0)
		ScrollingFrame.Position = UDim2.new(0, 0, 1, 0)
		ScrollingFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
		ScrollingFrame.ScrollBarThickness = 0

		UIListLayout.Parent = ScrollingFrame
		UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
		
		return ScrollingFrame
	end
	
	function UI:Button(Name_)
		local TextButton = Instance.new("TextButton")
		local Frame = Instance.new("Frame")
		local UICorner = Instance.new("UICorner")

		local MainTab = NewTab()
		
		table.insert(TabSystem["Buttons"], TextButton)

		local ButtonTabID = table.find(TabSystem["Buttons"], TextButton)

		if Name_ == nil or tostring(Name_) == nil then
			TextButton.Text = "No name was set."
		else
			TextButton.Text = Name_
		end
		TextButton.Parent = ScrollingFrame_Buttons
		TextButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
		TextButton.BackgroundTransparency = 1.000
		TextButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
		TextButton.BorderSizePixel = 0
		TextButton.ClipsDescendants = true
		TextButton.Size = UDim2.new(0.879999995, 0, 0.118749999, 0)
		TextButton.Font = Enum.Font.SourceSans
		TextButton.TextColor3 = Color3.fromRGB(237, 255, 251)
		TextButton.TextScaled = true
		TextButton.TextSize = 14.000
		TextButton.TextWrapped = true

		Frame.Parent = TextButton
		Frame.BackgroundColor3 = Color3.fromRGB(203, 255, 246)
		Frame.BorderColor3 = Color3.fromRGB(0, 0, 0)
		Frame.BorderSizePixel = 0
		Frame.Position = UDim2.new(-0.123000003, 0, -1, 0)
		Frame.Size = UDim2.new(0.181818187, 0, 1, 0)

		UICorner.CornerRadius = UDim.new(0, 3)
		UICorner.Parent = Frame

		TextButton.MouseButton1Click:Connect(function()
			if TabSystem["CurrentTab"][1] ~= ButtonTabID then
				local YValue = 0

				local OtherYValue = 0

				if TabSystem["CurrentTab"][1] > ButtonTabID then
					YValue = 1
					OtherYValue = -1
				elseif TabSystem["CurrentTab"][1] < ButtonTabID then
					YValue = -1
					OtherYValue = 1
				end

				if TabSystem["CurrentTab"][4] ~= nil then
					TabSystem["CurrentTab"][4]:Cancel()
					TweenService:Create(TabSystem["CurrentTab"][2], TweenScrollInfo, {Position = UDim2.new(-0.123000003, 0, OtherYValue, 0)}):Play()
				end

				if TabSystem["CurrentTab"][5] ~= nil then
					TabSystem["CurrentTab"][5]:Cancel()
					local TabToClose = TabSystem["CurrentTab"][3]
					local CloseTabTween = TweenService:Create(TabToClose, TweenTabInfo, {Position = UDim2.new(0, 0, YValue, 0)})
					CloseTabTween:Play()
					
					local TempEvent
					
					TempEvent = CloseTabTween.Completed:Connect(function()
						TabToClose.Visible = false
						TempEvent:Disconnect()
					end)
				end
				
				TabSystem["CurrentTab"][1] = ButtonTabID
				TabSystem["CurrentTab"][2] = Frame
				TabSystem["CurrentTab"][3] = MainTab

				Frame.Position = UDim2.new(-0.123000003, 0, YValue, 0)
				TabSystem["CurrentTab"][4] = TweenService:Create(Frame, TweenScrollInfo, {Position = UDim2.new(-0.123000003, 0, 0, 0)})
				TabSystem["CurrentTab"][4]:Play()
				
				MainTab.Position = UDim2.new(0, 0, OtherYValue, 0)
				MainTab.Visible = true
				TabSystem["CurrentTab"][5] = TweenService:Create(MainTab, TweenTabInfo, {Position = UDim2.new(0, 0, 0, 0)})
				TabSystem["CurrentTab"][5]:Play()
			end
		end)
		
		local ButtonTab = {}
		
		function ButtonTab:NewTitle(String)
			local Title = Instance.new("Frame")
			local TextLabel = Instance.new("TextLabel")
			
			local nilstring = ""

			if String == nil or tostring(String) == nil then
				TextLabel.Text = nilstring
			else
				TextLabel.Text = String
			end
			
			Title.Name = "Title"
			Title.Parent = MainTab
			Title.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Title.BackgroundTransparency = 1.000
			Title.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Title.BorderSizePixel = 0
			Title.Position = UDim2.new(0, 0, 0.194999993, 0)
			Title.Size = UDim2.new(1, 0, 0.165000007, 0)

			TextLabel.Parent = Title
			TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.BackgroundTransparency = 1.000
			TextLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
			TextLabel.BorderSizePixel = 0
			TextLabel.Position = UDim2.new(0.0390000008, 0, 0.104999997, 0)
			TextLabel.Size = UDim2.new(0.917647064, 0, 0.727272749, 0)
			TextLabel.Font = Enum.Font.SourceSans
			TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.TextScaled = true
			TextLabel.TextSize = 14.000
			TextLabel.TextTransparency = 0.400
			TextLabel.TextWrapped = true
			TextLabel.TextXAlignment = Enum.TextXAlignment.Left
		end
		
		function ButtonTab:NewButton(String,Call)
			local Button = Instance.new("Frame")
			local TextButton = Instance.new("TextButton")
			local UICorner = Instance.new("UICorner")
			
			local nilstring = ""
			
			if String == nil or tostring(String) == nil then
				TextButton.Text = nilstring
			else
				TextButton.Text = String
			end
			
			Button.Name = "Button"
			Button.Parent = MainTab
			Button.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Button.BackgroundTransparency = 1.000
			Button.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Button.BorderSizePixel = 0
			Button.Position = UDim2.new(0, 0, 0.194999993, 0)
			Button.Size = UDim2.new(1, 0, 0.165000007, 0)

			TextButton.Parent = Button
			TextButton.BackgroundColor3 = Color3.fromRGB(85, 170, 255)
			TextButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
			TextButton.BorderSizePixel = 0
			TextButton.Position = UDim2.new(0.0549019612, 0, 0.205128059, 0)
			TextButton.Size = UDim2.new(0.917647064, 0, 0.575757563, 0)
			TextButton.Font = Enum.Font.SourceSans
			TextButton.TextColor3 = Color3.fromRGB(0, 0, 0)
			TextButton.TextScaled = true
			TextButton.TextSize = 14.000
			TextButton.TextWrapped = true

			UICorner.Parent = TextButton
			
			TextButton.MouseButton1Click:Connect(function()
				pcall(Call)
			end)
		end
		
		function ButtonTab:NewText(String)
			local Text = Instance.new("Frame")
			local TextLabel = Instance.new("TextLabel")
			
			local nilstring = ""

			if String == nil or tostring(String) == nil then
				TextLabel.Text = nilstring
			else
				TextLabel.Text = String
			end
			
			Text.Name = "Text"
			Text.Parent = MainTab
			Text.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Text.BackgroundTransparency = 1.000
			Text.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Text.BorderSizePixel = 0
			Text.Position = UDim2.new(0, 0, 0.194999993, 0)
			Text.Size = UDim2.new(1, 0, 0.165000007, 0)

			TextLabel.Parent = Text
			TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.BackgroundTransparency = 1.000
			TextLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
			TextLabel.BorderSizePixel = 0
			TextLabel.Position = UDim2.new(0.0549019612, 0, 0.205128059, 0)
			TextLabel.Size = UDim2.new(0.917647064, 0, 0.575757563, 0)
			TextLabel.Font = Enum.Font.SourceSans
			TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.TextScaled = true
			TextLabel.TextSize = 14.000
			TextLabel.TextWrapped = true
			TextLabel.TextXAlignment = Enum.TextXAlignment.Left
		end
		
		function ButtonTab:NewSlider(String, Min, Max, SetValue)
			local Slider = Instance.new("Frame")
			local Frame = Instance.new("TextButton")
			local TextButton = Instance.new("TextButton")
			local UICorner = Instance.new("UICorner")
			local UICorner_2 = Instance.new("UICorner")
			local TextBox = Instance.new("TextBox")
			local TextLabel = Instance.new("TextLabel")
			
			local nilstring = ""

			if String == nil or tostring(String) == nil then
				TextLabel.Text = nilstring
			else
				TextLabel.Text = String
			end
			
			Slider.Name = "Slider"
			Slider.Parent = MainTab
			Slider.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Slider.BackgroundTransparency = 1.000
			Slider.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Slider.BorderSizePixel = 0
			Slider.Position = UDim2.new(0, 0, -0.0549999997, 0)
			Slider.Size = UDim2.new(1, 0, 0.325000048, 0)

			Frame.Name = "Frame"
			Frame.Parent = Slider
			Frame.BackgroundColor3 = Color3.fromRGB(37, 44, 57)
			Frame.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Frame.BorderSizePixel = 0
			Frame.Position = UDim2.new(0.0549019612, 0, 0.502564132, 0)
			Frame.Size = UDim2.new(0.800000012, 0, 0.333333671, 0)
			Frame.AutoButtonColor = false
			Frame.Font = Enum.Font.SourceSans
			Frame.Text = ""
			Frame.TextColor3 = Color3.fromRGB(0, 0, 0)
			Frame.TextSize = 14.000

			TextButton.Parent = Frame
			TextButton.BackgroundColor3 = Color3.fromRGB(85, 170, 255)
			TextButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
			TextButton.BorderSizePixel = 0
			TextButton.Size = UDim2.new(0.0588235296, 0, 1, 0)
			TextButton.AutoButtonColor = false
			TextButton.Font = Enum.Font.SourceSans
			TextButton.Text = ""
			TextButton.TextColor3 = Color3.fromRGB(0, 0, 0)
			TextButton.TextSize = 14.000

			UICorner.Parent = TextButton

			UICorner_2.Parent = Frame

			TextBox.Parent = Frame
			TextBox.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			TextBox.BackgroundTransparency = 1.000
			TextBox.BorderColor3 = Color3.fromRGB(0, 0, 0)
			TextBox.BorderSizePixel = 0
			TextBox.Position = UDim2.new(1.04186058, 0, 0, 0)
			TextBox.Size = UDim2.new(0.127450988, 0, 1, 0)
			TextBox.Font = Enum.Font.SourceSans
			TextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
			TextBox.TextScaled = true
			TextBox.TextSize = 14.000
			TextBox.TextWrapped = true

			TextLabel.Parent = Slider
			TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.BackgroundTransparency = 1.000
			TextLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
			TextLabel.BorderSizePixel = 0
			TextLabel.Position = UDim2.new(0.0549019612, 0, 0.112820424, 0)
			TextLabel.Size = UDim2.new(0.800000012, 0, 0.297435969, 0)
			TextLabel.Font = Enum.Font.SourceSans
			TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.TextScaled = true
			TextLabel.TextSize = 14.000
			TextLabel.TextWrapped = true
			TextLabel.TextXAlignment = Enum.TextXAlignment.Left
			
			local Frame = Frame
			local SliderButton = TextButton
			local TextBox = TextBox

			local buttonWidth = SliderButton.AbsoluteSize.X
			local buttonHalfWidth = buttonWidth / 2

			local dragging = false
			local inputChangedConn

			local SliderFunction = {}
			
			function SliderFunction:setSliderValue(value)
				local minPos = Frame.AbsolutePosition.X + buttonHalfWidth
				local maxPos = Frame.AbsolutePosition.X + Frame.AbsoluteSize.X - buttonHalfWidth

				local newPos = (value - Min) / (Max - Min) * (maxPos - minPos) + minPos
				SliderButton.Position = UDim2.new(0, newPos - Frame.AbsolutePosition.X - buttonHalfWidth, 0, 0)
				TextBox.Text = FixDecimals(tonumber(string.format("%.2f", value))) -- Display with two decimal places
			end

			local CurrentlyInFocus = false
			local PrevNumber = 0
			
			function SliderFunction:getValue()
				local NumValue = tonumber(TextBox.Text)
				if NumValue then
					return NumValue
				else
					return PrevNumber
				end
			end
			
			TextBox:GetPropertyChangedSignal("Text"):Connect(function()
				if CurrentlyInFocus == false then
					PrevNumber = SliderFunction:getValue()
				end
			end)
			
			Frame.MouseButton1Down:Connect(function()
				local newValue = tonumber(TextBox.Text)
				if newValue then
					if newValue > Max or newValue < Min then
						SliderButton.Visible = false
					else
						SliderButton.Visible = true
						SliderFunction:setSliderValue(newValue)
					end
				end
				dragging = true
			end)

			SliderButton.MouseButton1Down:Connect(function()
				local newValue = tonumber(TextBox.Text)
				if newValue then
					if newValue > Max or newValue < Min then
						SliderButton.Visible = false
					else
						SliderButton.Visible = true
						SliderFunction:setSliderValue(newValue)
					end
				end
				local newValue = FixDecimals(tonumber(TextBox.Text))
				dragging = true
			end)

			game:GetService("UserInputService").InputChanged:Connect(function(input)
				local newValue = tonumber(TextBox.Text)
				if newValue then
					if newValue > Max or newValue < Min then
						SliderButton.Visible = false
					else
						SliderButton.Visible = true
						SliderFunction:setSliderValue(newValue)
					end
				end
				if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
					local minPos = Frame.AbsolutePosition.X + buttonHalfWidth
					local maxPos = Frame.AbsolutePosition.X + Frame.AbsoluteSize.X - buttonHalfWidth

					local sliderPos = math.clamp(input.Position.X, minPos, maxPos)
					local sliderValue = Min + ((Max - Min) * (sliderPos - minPos) / (maxPos - minPos))

					SliderButton.Position = UDim2.new(0, sliderPos - Frame.AbsolutePosition.X - buttonHalfWidth, 0, 0)
					TextBox.Text = FixDecimals(tonumber(string.format("%.2f", sliderValue))) -- Display with two decimal places
				end
			end)

			game:GetService("UserInputService").InputEnded:Connect(function(input)
				local newValue = tonumber(TextBox.Text)
				if newValue then
					if newValue > Max or newValue < Min then
						SliderButton.Visible = false
					else
						SliderButton.Visible = true
						SliderFunction:setSliderValue(newValue)
					end
				end
				if input.UserInputType == Enum.UserInputType.MouseButton1 then
					dragging = false
				end
			end)
			
			local TempConnection
			
			--somehow the focused event works once and never again.
			
			local function newconnection()
				if TempConnection ~= nil then
					TempConnection:Disconnect()
					TempConnection = nil
				end
				TempConnection = TextBox.Focused:Connect(function()
					CurrentlyInFocus = true
				end)
			end
			
			TextBox.FocusLost:Connect(function()
				local newValue = tonumber(TextBox.Text)
				if newValue then
					if newValue > Max or newValue < Min then
						SliderButton.Visible = false
					else
						SliderButton.Visible = true
						SliderFunction:setSliderValue(newValue)
					end
				else
					TextBox.Text = FixDecimals(tonumber(string.format("%.2f", 0)))
					SliderFunction:setSliderValue(0)
				end
				CurrentlyInFocus = false
				newconnection()
			end)

			if SetValue == nil then
				SliderFunction:setSliderValue(0)
			else
				SliderFunction:setSliderValue(SetValue)
			end
			
			return SliderFunction
		end
		
		function ButtonTab:NewToggle(String)
			local ToggleFunctions = {}
			local Toggled = false
			
			local Toggle = Instance.new("Frame")
			local TextLabel = Instance.new("TextLabel")
			local TextButton = Instance.new("TextButton")
			local UICorner = Instance.new("UICorner")
			
			local nilstring = ""

			if String == nil or tostring(String) == nil then
				TextLabel.Text = nilstring
			else
				TextLabel.Text = String
			end
			
			Toggle.Name = "Toggle"
			Toggle.Parent = MainTab
			Toggle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Toggle.BackgroundTransparency = 1.000
			Toggle.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Toggle.BorderSizePixel = 0
			Toggle.Position = UDim2.new(0, 0, 0.194999993, 0)
			Toggle.Size = UDim2.new(1, 0, 0.165000007, 0)

			TextLabel.Parent = Toggle
			TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.BackgroundTransparency = 1.000
			TextLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
			TextLabel.BorderSizePixel = 0
			TextLabel.Position = UDim2.new(0.0549019612, 0, 0.205128208, 0)
			TextLabel.Size = UDim2.new(0.800000012, 0, 0.575757563, 0)
			TextLabel.Font = Enum.Font.SourceSans
			TextLabel.Text = "Toggle"
			TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.TextScaled = true
			TextLabel.TextSize = 14.000
			TextLabel.TextWrapped = true
			TextLabel.TextXAlignment = Enum.TextXAlignment.Left

			TextButton.Parent = Toggle
			TextButton.BackgroundColor3 = Color3.fromRGB(255, 70, 70)
			TextButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
			TextButton.BorderSizePixel = 0
			TextButton.Position = UDim2.new(0.90196079, 0, 0.205128208, 0)
			TextButton.Size = UDim2.new(0.0705882385, 0, 0.575757563, 0)
			TextButton.AutoButtonColor = false
			TextButton.Font = Enum.Font.SourceSans
			TextButton.Text = ""
			TextButton.TextColor3 = Color3.fromRGB(0, 0, 0)
			TextButton.TextSize = 14.000

			UICorner.Parent = TextButton
			local Tweening = nil
			
			TextButton.MouseButton1Click:Connect(function()
				Toggled = not Toggled
				if Toggled == false then
					if Tweening ~= nil then
						Tweening:Cancel()
						TextButton.BackgroundColor3 = Color3.fromRGB(170, 255, 127)
					end
					Tweening = TweenService:Create(TextButton, TweenColorToggleInfo, {BackgroundColor3 = Color3.fromRGB(255, 70, 70)})
					Tweening:Play()
				elseif Toggled == true then
					if Tweening ~= nil then
						Tweening:Cancel()
						TextButton.BackgroundColor3 = Color3.fromRGB(255, 70, 70)
					end
					Tweening = TweenService:Create(TextButton, TweenColorToggleInfo, {BackgroundColor3 = Color3.fromRGB(170, 255, 127)})
					Tweening:Play()
				end
			end)
			
			function ToggleFunctions:setBoolValue(bool)
				Toggled = bool
				if Toggled == false then
					if Tweening ~= nil then
						Tweening:Cancel()
						TextButton.BackgroundColor3 = Color3.fromRGB(170, 255, 127)
					end
					Tweening = TweenService:Create(TextButton, TweenColorToggleInfo, {BackgroundColor3 = Color3.fromRGB(255, 70, 70)})
					Tweening:Play()
				elseif Toggled == true then
					if Tweening ~= nil then
						Tweening:Cancel()
						TextButton.BackgroundColor3 = Color3.fromRGB(255, 70, 70)
					end
					Tweening = TweenService:Create(TextButton, TweenColorToggleInfo, {BackgroundColor3 = Color3.fromRGB(170, 255, 127)})
					Tweening:Play()
				end
			end
			
			function ToggleFunctions:getBoolValue()
				return Toggled
			end
			
			return ToggleFunctions
		end
		
		function ButtonTab:NewDropDown(TableList, SelectValue)
			if TableList ~= nil then
				local MainList = {}
				
				local Dropdown = Instance.new("Frame")
				local TextButton = Instance.new("TextButton")
				local UICorner = Instance.new("UICorner")
				local TextLabel = Instance.new("TextLabel")
				local Frame = Instance.new("Frame")
				local ImageLabel = Instance.new("ImageLabel")
				local ScrollingFrame = Instance.new("ScrollingFrame")
				local UIListLayout = Instance.new("UIListLayout")
				local UIListLayout_2 = Instance.new("UIListLayout")

				Dropdown.Name = "Dropdown"
				Dropdown.Parent = MainTab
				Dropdown.AutomaticSize = Enum.AutomaticSize.Y
				Dropdown.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				Dropdown.BackgroundTransparency = 1.000
				Dropdown.BorderColor3 = Color3.fromRGB(0, 0, 0)
				Dropdown.BorderSizePixel = 0
				Dropdown.Position = UDim2.new(0, 0, 0.524999976, 0)
				Dropdown.Size = UDim2.new(1, 0, 0.173750073, 0)

				TextButton.Parent = Dropdown
				TextButton.LayoutOrder = -1
				TextButton.BackgroundColor3 = Color3.fromRGB(37, 44, 57)
				TextButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
				TextButton.BorderSizePixel = 0
				TextButton.Position = UDim2.new(0.918, 0,0.45, 0)
				TextButton.Size = UDim2.new(0.917999983, 0, 0.449999988, 0)
				TextButton.ZIndex = 2
				TextButton.AutoButtonColor = false
				TextButton.Font = Enum.Font.SourceSans
				TextButton.Text = ""
				TextButton.TextColor3 = Color3.fromRGB(255, 255, 255)
				TextButton.TextScaled = true
				TextButton.TextSize = 14.000
				TextButton.TextWrapped = true

				UICorner.CornerRadius = UDim.new(0, 4)
				UICorner.Parent = TextButton

				TextLabel.Parent = TextButton
				TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				TextLabel.BackgroundTransparency = 1.000
				TextLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
				TextLabel.BorderSizePixel = 0
				TextLabel.Size = UDim2.new(1, 0, 1, 0)
				TextLabel.ZIndex = 2
				TextLabel.Font = Enum.Font.SourceSans
				TextLabel.Text = "nil"
				TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
				TextLabel.TextScaled = true
				TextLabel.TextSize = 14.000
				TextLabel.TextWrapped = true

				Frame.Parent = TextButton
				Frame.BackgroundColor3 = Color3.fromRGB(37, 44, 57)
				Frame.BorderColor3 = Color3.fromRGB(0, 0, 0)
				Frame.BorderSizePixel = 0
				Frame.Position = UDim2.new(0, 0, 0.684210539, 0)
				Frame.Size = UDim2.new(1, 0, 0.368421048, 0)
				Frame.Visible = false

				ImageLabel.Parent = TextButton
				ImageLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
				ImageLabel.BackgroundTransparency = 1.000
				ImageLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
				ImageLabel.BorderSizePixel = 0
				ImageLabel.Position = UDim2.new(0.899999976, 0, 0, 0)
				ImageLabel.Size = UDim2.new(0.0854700878, 0, 1.05263162, 0)
				ImageLabel.Image = "rbxassetid://12974422850"

				ScrollingFrame.Parent = Dropdown
				ScrollingFrame.Active = true
				ScrollingFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
				ScrollingFrame.CanvasSize = UDim2.new(0,0,0,0)
				ScrollingFrame.BackgroundColor3 = Color3.fromRGB(37, 44, 57)
				ScrollingFrame.BorderColor3 = Color3.fromRGB(0, 0, 0)
				ScrollingFrame.BorderSizePixel = 0
				ScrollingFrame.Position = UDim2.new(0.918, 0,0, 0)
				ScrollingFrame.Size = UDim2.new(0.917999983, 0, 0, 0)
				ScrollingFrame.Visible = false
				ScrollingFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
				ScrollingFrame.ScrollBarThickness = 10
				
				UIListLayout.Parent = ScrollingFrame
				UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
				
				UIListLayout_2.Parent = Dropdown
				UIListLayout_2.HorizontalAlignment = Enum.HorizontalAlignment.Center
				UIListLayout_2.SortOrder = Enum.SortOrder.LayoutOrder
				UIListLayout_2.VerticalAlignment = Enum.VerticalAlignment.Center
				
				local DropDownFunctions = {}
				local SelectedValue = nil
				
				function DropDownFunctions:setNewValue(Arg)
					if tostring(Arg) then
						local DropdownButton = CreateNewDropdownButton(tostring(Arg), ScrollingFrame)
						local i = #MainList + 1
						
						MainList[i] = {}
						MainList[i]["Value"] = Arg
						MainList[i]["Button"] = DropdownButton

						DropdownButton.MouseButton1Click:Connect(function()
							SelectedValue = SelectedValue
							TextLabel.Text = tostring(Arg)
						end)
					end
				end
				
				function DropDownFunctions:removeValue(Arg)
					for _, v in pairs(MainList) do
						if v["Value"] == Arg then
							v["Button"]:Destroy()
							table.remove(MainList, v)
						end
					end
				end
				
				function DropDownFunctions:selectValue(Arg)
					for _, v in pairs(MainList) do
						if v["Value"] == Arg then
							SelectedValue = Arg
						end
					end
				end
				
				function DropDownFunctions:getValue()
					return SelectedValue
				end
				
				for i, v in pairs(TableList) do
					if tostring(v) then
						local DropdownButton = CreateNewDropdownButton(tostring(v), ScrollingFrame)
						
						MainList[i] = {}
						MainList[i]["Value"] = v
						MainList[i]["Button"] = DropdownButton
						
						DropdownButton.MouseButton1Click:Connect(function()
							SelectedValue = v
							TextLabel.Text = tostring(v)
						end)
					end
				end
				
				if SelectValue ~= nil then
					DropDownFunctions:selectValue(SelectValue)
				end
				
				local Tweening = nil
				local Tweening1, Tweening2 = nil, nil
				local Opened = false

				local TempConnection

				TextButton.MouseButton1Click:Connect(function()
					Opened = not Opened
					if TempConnection ~= nil then
						TempConnection:Disconnect()
						TempConnection = nil
					end
					if Opened == true then
						ScrollingFrame.Visible = true
						if Tweening ~= nil then
							ImageLabel.Rotation = 0
							Tweening:Cancel()
							Tweening = nil
						end
						if Tweening1 ~= nil then
							Tweening1:Cancel()
							Tweening1 = nil
						end
						if Tweening2 ~= nil then
							Tweening2:Cancel()
							Tweening2 = nil
						end

						Tweening = TweenService:Create(ImageLabel, TweenDropDownInfo, {Rotation = 180})
						Tweening:Play()

						Frame.Visible = true

						Tweening1 = TweenService:Create(TextButton, TweenDropDownInfo, {Size = UDim2.new(0.918, 0, 0.269, 0)})
						Tweening1:Play()

						Tweening2 = TweenService:Create(ScrollingFrame, TweenDropDownInfo, {Size = UDim2.new(0.918, 0, 0.486, 0)})
						Tweening2:Play()
					elseif Opened == false then
						if Tweening ~= nil then
							ImageLabel.Rotation = 180
							Tweening:Cancel()
							Tweening = nil
						end
						if Tweening1 ~= nil then
							Tweening1:Cancel()
							Tweening1 = nil
						end
						if Tweening2 ~= nil then
							Tweening2:Cancel()
							Tweening2 = nil
						end
						Frame.Visible = true

						Tweening = TweenService:Create(ImageLabel, TweenDropDownInfo, {Rotation = 360})
						Tweening:Play()

						Tweening1 = TweenService:Create(TextButton, TweenDropDownInfo, {Size = UDim2.new(0.918, 0, 0.45, 0)})
						Tweening1:Play()

						Tweening2 = TweenService:Create(ScrollingFrame, TweenDropDownInfo, {Size = UDim2.new(0.918, 0, 0, 0)})
						Tweening2:Play()

						TempConnection = Tweening.Completed:Connect(function()
							ImageLabel.Rotation = 0
							Frame.Visible = false
							ScrollingFrame.Visible = false
						end)
					end
				end)
				
				return DropDownFunctions
			end
		end
		return ButtonTab
	end

	return UI
end

function BasicLibrary:UserNotify(String, Duration)
	if NotificationsList == nil then
		CreateList()
	end
	
	if Duration and String and tostring(String) then
		coroutine.wrap(function()
			local NotificationRoot = Instance.new("Frame")
			local Notification = Instance.new("Frame")
			local Frame = Instance.new("Frame")
			local Frame_2 = Instance.new("Frame")
			local TextLabel = Instance.new("TextLabel")

			local nilstring = ""

			if String == nil or tostring(String) == nil then
				TextLabel.Text = nilstring
			else
				TextLabel.Text = String
			end

			NotificationRoot.Name = "NotificationRoot"
			NotificationRoot.Parent = NotificationsList
			NotificationRoot.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			NotificationRoot.BackgroundTransparency = 1.000
			NotificationRoot.BorderColor3 = Color3.fromRGB(0, 0, 0)
			NotificationRoot.BorderSizePixel = 0
			NotificationRoot.Position = UDim2.new(0.729341328, 0, 0.925344169, 0)
			NotificationRoot.Size = UDim2.new(1, 0, 0.0549999997, 0)

			Notification.Name = "Notification"
			Notification.Parent = NotificationRoot
			Notification.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			Notification.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Notification.Position = UDim2.new(1,0,0,0)
			Notification.BorderSizePixel = 0
			Notification.Size = UDim2.new(1, 0, 1, 0)

			Frame.Parent = Notification
			Frame.Position = UDim2.new(1,0,0,0)
			Frame.BackgroundColor3 = Color3.fromRGB(85, 170, 255)
			Frame.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Frame.BorderSizePixel = 0
			Frame.Size = UDim2.new(1, 0, 1, 0)

			Frame_2.Parent = Frame
			Frame_2.Position = UDim2.new(1,0,0,0)
			Frame_2.BackgroundColor3 = Color3.fromRGB(37, 44, 57)
			Frame_2.BorderColor3 = Color3.fromRGB(0, 0, 0)
			Frame_2.BorderSizePixel = 0
			Frame_2.ClipsDescendants = true
			Frame_2.Size = UDim2.new(1, 0, 1, 0)

			TextLabel.Parent = Frame_2
			TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.BackgroundTransparency = 1.000
			TextLabel.BorderColor3 = Color3.fromRGB(0, 0, 0)
			TextLabel.BorderSizePixel = 0
			TextLabel.Position = UDim2.new(0,0,0.148,0)
			TextLabel.Size = UDim2.new(0.969026625, 0, 0.703703701, 0)
			TextLabel.Font = Enum.Font.SourceSans
			TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
			TextLabel.TextScaled = true
			TextLabel.TextSize = 14.000
			TextLabel.TextWrapped = true

			local WhiteAnim = TweenService:Create(Notification, NotifyTweenInfo, {Position = UDim2.new(0,0,0,0)})
			local FrameAnim = TweenService:Create(Frame, NotifyCatchUpInfo, {Position = UDim2.new(0,0,0,0)})
			local Frame2Anim = TweenService:Create(Frame_2, NotifyCatchUpInfo, {Position = UDim2.new(0.031,0,0,0)})

			WhiteAnim:Play()
			WhiteAnim.Completed:Wait()
			FrameAnim:Play()
			task.wait(0.2)
			Frame2Anim:Play()
			Frame2Anim.Completed:Wait()
			task.wait(Duration)
			
			local WhiteAnim_Exit = TweenService:Create(Notification, NotifyTweenInfo, {Position = UDim2.new(1,0,0,0)})
			local FrameAnim_Exit = TweenService:Create(Frame, NotifyCatchUpInfo, {Position = UDim2.new(1,0,0,0)})
			local Frame2Anim_Exit = TweenService:Create(Frame_2, NotifyCatchUpInfo, {Position = UDim2.new(1,0,0,0)})

			Frame2Anim_Exit:Play()
			task.wait(0.2)
			FrameAnim_Exit:Play()
			FrameAnim_Exit.Completed:Wait()
			WhiteAnim_Exit:Play()

			WhiteAnim_Exit.Completed:Wait()
			NotificationRoot:Destroy()
		end)()
	end
end

return BasicLibrary
