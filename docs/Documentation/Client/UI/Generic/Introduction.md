# Generic
Generic is a framework for creating UIs using just lua scripting. It functions by instancing a special .swf with various types of *elements* implemented that you can then interface with from lua.

It offers various advantages over traditional UI creation:

- **No fiddling with flash**: UI creation with Generic uses purely lua. You do not need to touch or know anything about flash files.
- **Extendability and moddability**: UIs made with Generic, along with their elements, are exposed to all mods; any script can hook these UIs to add elements to them or modify them, something not possible with .swf UIs.
- **Fast prototyping**: all you need to do to test your changes to the UI is to reload lua. There is no requirement for external tools nor any exporting process.

Generic powers every UI in Epip made after its inception, including:

- Quick Examine
- Hotbar Groups
- Save/Load Overlay
- Debug Display
- Debug Menu / Control Panel
- Fishing minigame

## Getting started
TODO

## Prefabs
TODO

## Classes

<doc class="GenericUI" symbols="_SubClasses">

```lua
---@class GenericUI_Instance

---@param id string
---@return GenericUI_Element? 
function _Instance:GetElementByID(id)

---@param element GenericUI_Element
function _Instance:DestroyElement(element)

---@param id string
---@return FlashMovieClip? 
function _Instance:GetMovieClipByID(id)

---@param id string
---@param elementType `T`|GenericUI_ElementType
---@param parentID string|GenericUI_Element? Defaults to root of the MainTimeline.
---@return `T` 
function _Instance:CreateElement(id, elementType, parentID)

---@return number, number
function _Instance:GetMousePosition()

```
```lua
---@class GenericUI_Prefab

---@param id string Automatically prefixed.
---@param elementType `T`|GenericUI_ElementType
---@param parent (GenericUI_Element|string)?
---@return T 
function Prefab:CreateElement(id, elementType, parent)

function Prefab:PrefixID(id)

function Prefab:GetMainElement()

function Prefab:Destroy()

```
```lua
---@class GenericUI_ContainerElement
---@field ClearElements fun(self) Removes all elements from the container.

```
```lua
---@class GenericUI_Element
---@field UI GenericUI_Instance
---@field ID string
---@field ParentID string Empty string for elements in the root.
---@field Type string
---@field Tooltip (GenericUI_ElementTooltip|string)? Will be rendered upon the element being hovered. Strings are rendered as unformatted tooltips.
---@field SetPositionRelativeToParent fun(self:GenericUI_Element, position:"Center"|"TopLeft"|"TopRight"|"Top"|"Left"|"Right"|"BottomLeft"|"Bottom"|"BottomRight", horizontalOffset:number?, verticalOffset:number?)
---@field Move fun(self:GenericUI_Element, x:number, y:number) Moves the element a certain amount of pixels from its current position.
---@field Events GenericUI_Element_Events
---@field _Tooltip GenericUI_ElementTooltip

---Get the movie clip of this element.
---@return FlashMovieClip 
function _Element:GetMovieClip()

---@param id string
---@param elementType `T`|GenericUI_ElementType
---@return `T` 
function _Element:AddChild(id, elementType)

---Sets whether the element should be horizontally centered in VerticalList and ScrollList.
---@param center boolean
function _Element:SetCenterInLists(center)

---Sets this element as the area for dragging the *entire* UI.
function _Element:SetAsDraggableArea()

---@param x number
---@param y number
function _Element:SetPosition(x, y)

---@param width number
---@param height number
function _Element:SetSize(width, height)

---@param enabled boolean
function _Element:SetMouseEnabled(enabled)

---@param enabled boolean
function _Element:SetMouseChildren(enabled)

---@param alpha number
---@param affectChildren boolean? Defaults to not affecting children alpha.
function _Element:SetAlpha(alpha, affectChildren)

---@param degrees number
function _Element:SetRotation(degrees)

function _Element:Destroy()

---@param eventType string
---@param handler function
function _Element:RegisterListener(eventType, handler)

---@return number, number -- X and Y coordinates in local space.
function _Element:GetPosition()

---@param visible boolean
function _Element:SetVisible(visible)

---@param tween GenericUI_ElementTween
function _Element:Tween(tween)

---Sets the size override, used to override the element size within list-like elements.
---@overload fun(self:GenericUI_Element, size:Vector2) 
---@param width number
---@param height number
function _Element:SetSizeOverride(width, height)

---Sets the scroll rect of the element.
---@param position Vector2
---@param size Vector2
function _Element:SetScrollRect(position, size)

---Removes the scroll rect from the element, if any.
function _Element:RemoveScrollRect()

---Sets the Z-order index of a child element.
---@param child string|GenericUI_Element
---@param index integer
function _Element:SetChildIndex(child, index)

---Returns the calculated width of the element.
---@return number 
function _Element:GetWidth()

---Returns the calculated height of the element.
---@return number 
function _Element:GetHeight()

---Sets the scale of the element.
---@param scale Vector2
function _Element:SetScale(scale)

---Returns the scale of the element.
---@return Vector2 
function _Element:GetScale()

---Sets the tooltip of the element.
---@param tooltipType TooltipLib_TooltipType
---@param tooltip any TODO document
function _Element:SetTooltip(tooltipType, tooltip)

```
```lua
---TODO!
---@class GenericUI_ElementTooltip
---@field Type TooltipLib_TooltipType

```
```lua
---@class GenericUI_ElementTween
---@field EventID string
---@field Duration number
---@field Type "To"
---@field StartingValues table<string, any> Maps property to starting value.
---@field FinalValues table<string, any> Maps property to final value.
---@field Function "Linear"|"Quadratic"|"Cubic"|"Quartic"|"Sine"|"Elastic"
---@field Ease "EaseNone"|"EaseIn"|"EaseOut"|"EaseInOut"
---@field Delay number? Defaults to 0 seconds.
---@field OnComplete fun(ev:GenericUI_Element_Event_TweenCompleted)? Shorthand for registering a TweenCompleted listener. Will run only once, then be unsubscribed.

```
```lua
---@class GenericUI_Element_Empty

---@class GenericUI_Element_Empty

```
```lua
---@class GenericUI_Element_TiledBackground

---Sets the background's visuals and size.
---@param bg GenericUI_Element_TiledBackground_Type
---@param width number
---@param height number
function Background:SetBackground(bg, width, height)

---@class GenericUI_Element_TiledBackground
---@field Events GenericUI_Element_Events

```
```lua
---@class GenericUI_Element_Text

---Sets the element's text.
---Note that the text will be culled if it doesn't fit the dimensions of the element.
---@param text string
---@param setSize boolean? Defaults to `false`. If `true`, the element will be automatically resized to fit the new text.
function Text:SetText(text, setSize)

---Sets the alignment of the text.
---@param textType GenericUI_Element_Text_Align
function Text:SetType(textType)

---Sets whether the text is editable by the user.
---@param editable boolean
function Text:SetEditable(editable)

---Sets the restriction for characters that the user can enter onto the text field.
---Has no effect on setting the text from scripting.
---@param restriction string
function Text:SetRestrictedCharacters(restriction)

---@class GenericUI_Element_Text
---@field Events GenericUI_Element_Text_Events

---Sets the stroke style and color of the text element.
---@param color uint64|RGBColor
---@param size number
---@param alpha number
---@param strength uint64
---@param unknown uint64
function Text:SetStroke(color, size, alpha, strength, unknown)

---Returns the size of the text itself.
---@return Vector2 
function Text:GetTextSize()

---Sets whether text should wrap once it reaches the edge of the element's size.
---@param wrap boolean
function Text:SetWordWrap(wrap)

```
```lua
---@class GenericUI_Element_IggyIcon

---@class GenericUI_Element_IggyIcon
---@field SetIcon fun(self, icon:string, width:number, height:number, materialGUID:GUID?)

---Sets the icon displayed by the element.
---@param icon string
---@param width number
---@param height number
---@param materialGUID GUID?
function IggyIcon:SetIcon(icon, width, height, materialGUID)

```
```lua
---@class GenericUI_Element_Button

---Sets the button's text.
---@param text string
---@param textY number? Vertical offset for the text. Use for centering.
function Button:SetText(text, textY)

---Sets the button's visuals.
---@param buttonType GenericUI_Element_Button_Type
function Button:SetType(buttonType)

---Sets the button's enabled state. Enabled buttons are interactable.
---@param enabled boolean
function Button:SetEnabled(enabled)

---Returns whether the button is enabled.
---@return boolean 
function Button:IsEnabled()

---@class GenericUI_Element_Button
---@field Events GenericUI_Element_Button_Events

```
```lua
---@class GenericUI_Element_VerticalList

---Removes all elements from the container.
function VerticalList:Clear()

---Repositions all the elements within the container.
---Does not recursively reposition parented containers. TODO
function VerticalList:RepositionElements()

---Sets a padding to be placed before the first element of the container.
---@param spacing number
function VerticalList:SetTopSpacing(spacing)

---Sets the spacing between positioned elements.
---@param spacing number
function VerticalList:SetElementSpacing(spacing)

---Sets a padding for the left side of the container.
---@param spacing number
function VerticalList:SetSideSpacing(spacing)

---Sets whether all elements within the list should be repositioned after adding a new one.
---Default behaviour is to do so; disabling it offers far better performance when bulk-adding elements.
---@param reposition boolean
function VerticalList:SetRepositionAfterAdding(reposition)

---@class GenericUI_Element_VerticalList

```
```lua
---@class GenericUI_Element_HorizontalList

---@class GenericUI_Element_HorizontalList

```
```lua
---@class GenericUI_Element_ScrollList

---Sets the size of the scroll list. Contents outside the rect will be culled.
---@param width number
---@param height number
function ScrollList:SetFrame(width, height)

---Sets whether the scroll list can be scrolled with the mouse wheel.
---@param enabled boolean
function ScrollList:SetMouseWheelEnabled(enabled)

---Sets the horizontal spacing for the scroll bar, relative to the right edge of the frame.
---Must be called after SetFrame. TODO remove restriction
---@param spacing number
function ScrollList:SetScrollbarSpacing(spacing)

---@class GenericUI_Element_ScrollList

```
```lua
---@class GenericUI_Element_StateButton

---Sets the button's visuals.
---@param buttonType GenericUI_Element_StateButton_Type
function StateButton:SetType(buttonType)

---Sets whether the button is active.<br>
---This has no intrinsic meaning, other than altering the button's graphics.
---@param active boolean
function StateButton:SetActive(active)

---Sets whether the button is enabled.<br>
---Enabled buttons are interactable and their active state can be changed by the user.
---@param enabled boolean
function StateButton:SetEnabled(enabled)

---@class GenericUI_Element_StateButton
---@field Events GenericUI_Element_StateButton_Events

```
```lua
---@class GenericUI_Element_Divider
---@meta 

---Sets the visual for the divider.
---@param dividerType GenericUI_Element_Divider_Type
function Divider:SetType(dividerType)

---Sets the size of the divider.
---Custom height not currently supported. TODO
---@param width number
function Divider:SetSize(width)

---@class GenericUI_Element_Divider

```
```lua
---@class GenericUI_Element_Slot

---Sets the cooldown displayed by the slot.
---@param cooldown number In turns.
---@param playRefreshAnimation boolean? Defaults to false. If set to true and the cooldown is <= 0, a blink animation will be played.
function Slot:SetCooldown(cooldown, playRefreshAnimation)

---Sets whether the slot is enabled. Disabled slots are greyed out.
---@param enabled boolean
function Slot:SetEnabled(enabled)

---Sets the label shown on the bottom right of the slot.
---@param label string
function Slot:SetLabel(label)

---Sets whether the slot should display a blue border.
---@param enabled boolean
function Slot:SetSourceBorder(enabled)

---Sets whether the slot should display a warning graphic.
---@param enabled boolean
function Slot:SetWarning(enabled)

---Sets whether the slot is active. Active slots play a looping ripple animation.
---@param active boolean
function Slot:SetActive(active)

---Sets whether the slot is highlighted.
---@param highlighted boolean
function Slot:SetHighlighted(highlighted)

---@class GenericUI_Element_Slot
---@field Events GenericUI_Element_Slot_Events

```
```lua
---@class GenericUI_Element_Slider

---@class GenericUI_Element_Slider
---@field Events GenericUI_Element_Slider_Events

---Returns the current value selected in the slider.
---@return number 
function Slider:GetValue()

---Sets the value of the slider.
---@param value number
function Slider:SetValue(value)

---Sets whether the slider should use notches and snap to them.
---@param useNotches boolean Default behaviour is `false`.
function Slider:SetUseNotches(useNotches)

---Sets the minimum value accepted by the slider.
---@param min number
function Slider:SetMin(min)

---Sets the maximum value accepted by the slider.
---@param max number
function Slider:SetMax(max)

---Sets the step interval of the slider.
---@param step number
function Slider:SetStep(step)

```
```lua
---@class GenericUI_Element_ComboBox

---Sets the currently selected option.
---@param id string
function ComboBox:SelectOption(id)

---Removes all options from the combobox.
function ComboBox:ClearOptions()

---Sets whether the combobox should open upwards, or downwards (default)
---Use to determine the orientation of the options selector when opened.
---@param openUpwards boolean
function ComboBox:SetOpenUpwards(openUpwards)

---@class GenericUI_Element_ComboBox
---@field _Options GenericUI_Element_ComboBox_Option[]
---@field Events GenericUI_Element_ComboBox_Events

---Sets the options for the combobox. Equivalent to calling `ClearOptions()` then `AddOption()` for each option in the list passed.
---@param options GenericUI_Element_ComboBox_Option[]
function ComboBox:SetOptions(options)

---Adds an option to the combobox.
---@param id string
---@param label string
function ComboBox:AddOption(id, label)

```
```lua
---Represents an option in the combobox.
---@class GenericUI_Element_ComboBox_Option
---@field Label string
---@field ID string

```
```lua
---@class GenericUI_Element_Grid

---Sets the size of the grid, in elements.
---@param columns integer Set to -1 for infinite.
---@param rows integer Set to -1 for infinite.
function Grid:SetGridSize(columns, rows)

---Sets whether all elements within the list should be repositioned after adding a new one.
---Default behaviour is to do so; disabling it offers far better performance when bulk-adding elements.
---@param reposition boolean
function Grid:SetRepositionAfterAdding(reposition)

---@class GenericUI_Element_Grid

---Sets the spacing between elements.
---@param row number
---@param column number
function Grid:SetElementSpacing(row, column)

```
```lua
---@class GenericUI_Element_Color

---@class GenericUI_Element_Color

---Sets the color shown by the element.
---@param color RGBColor
function Color:SetColor(color)

```
```lua
---@class GenericUI_Element_Texture

---@class GenericUI_Element_Texture

---Sets the texture resource used.
---@param guid GUID
---@param size Vector2? Defaults to native size of the texture resource.
function Texture:SetTexture(guid, size)

```
```lua
---@class GenericUI_Prefab_HotbarSlot
---@field SlotIcon GenericUI_Element_IggyIcon
---@field RarityIcon GenericUI_Element_IggyIcon
---@field RuneSlotsIcon GenericUI_Element_IggyIcon
---@field _CanDrag boolean
---@field _CanDrop boolean
---@field _ClearAfterDrag boolean
---@field _AutoUpdateDelay number In seconds.
---@field _AutoUpdateRemainingDelay number In seconds.

---@param ui GenericUI_Instance
---@param id string
---@param parent GenericUI_Element
---@return GenericUI_Prefab_HotbarSlot 
function Slot.Create(ui, id, parent)

---@param obj GenericUI_Prefab_HotbarSlot_Object
function Slot:SetObject(obj)

---@param skillID string
function Slot:SetSkill(skillID)

---@param item EclItem
function Slot:SetItem(item)

---Sets the label of the slot, displayed in the bottom right corner.
---@param label string
function Slot:SetLabel(label)

---Sets the icon of the slot.
---@param icon icon
---@param size Vector2?
function Slot:SetIcon(icon, size)

---Sets the rarity frame.
---@param rarity ItemLib_Rarity|EclItem
function Slot:SetRarityIcon(rarity)

---Sets the slot to contain an item template.
---Does not set rarity icon by design (since the player could have multiple items of the same template with varying rarities).
---@param templateID GUID
function Slot:SetTemplate(templateID)

---Sets the enabled state of the slot.
---@param enabled boolean
function Slot:SetEnabled(enabled)

---Sets the cooldown displayed on the slot.
---@param cooldown number In turns.
---@param playRefreshAnimation boolean? Defaults to `false`.
function Slot:SetCooldown(cooldown, playRefreshAnimation)

---Sets whether the slot can be interacted with to use its object.
---Default behaviour is to allow usage.
---@param usable boolean
function Slot:SetUsable(usable)

function Slot:Clear()

---Sets whether objects can be dragged out of the slot.
---@param canDrag boolean
---@param clearSlotAfterwards boolean? Whether to clear the slot when dragging out. Defaults to same value as `canDrag`.
function Slot:SetCanDrag(canDrag, clearSlotAfterwards)

---Sets whether objects can be dragged onto the slot to assign them.
---@param canDrop boolean
function Slot:SetCanDrop(canDrop)

---Sets whether entities can be dragged in and out of the slot.
---@param canDragDrop boolean
function Slot:SetCanDragDrop(canDragDrop)

---Sets the time between the element being automatically updated with data of its set entity.
---@param delay number In seconds. Set to `-1` to disable.
function Slot:SetUpdateDelay(delay)

---Returns whether the slot currently holds no object.
---@return boolean 
function Slot:IsEmpty()

```
```lua
---@class GenericUI_Prefab_HotbarSlot_Object
---@field Type GenericUI_Prefab_HotbarSlot_Object_Type
---@field StatsID string? Only for skills/actions.
---@field ItemHandle EntityHandle? Only for items.
---@field TemplateID GUID? Only for templates.

---@param type GenericUI_Prefab_HotbarSlot_Object_Type
---@param data GenericUI_Prefab_HotbarSlot_Object?
---@return GenericUI_Prefab_HotbarSlot_Object 
function _SlotObject.Create(type, data)

---Returns the entity assigned to the slot.
---@return EclItem|StatsLib_SkillData|StatsLib_Action 
function _SlotObject:GetEntity()

```
```lua
---@class GenericUI_Prefab_Spinner

---Creates a Spinner element.
---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param label string
---@param min number? Defaults to 0.
---@param max number? Defaults to math.maxinteger.
---@param step number? Defaults to 1.
---@return GenericUI_Prefab_Spinner 
function Spinner.Create(ui, id, parent, label, min, max, step)

---@return number 
function Spinner:GetValue()

---Sets the value of the spinner. Ignores min/max bounds or step.
---@param value number
function Spinner:SetValue(value)

---@return number 
function Spinner:Decrement()

---Adds to the current value. **Throws the ValueChanged event!**
---@param val number
---@return number New value.
function Spinner:AddValue(val)

---@return number 
function Spinner:Increment()

function Spinner:UpdateCounter()

---Sets the bounds of the allowed values on the spinner and clamps the current value to the new valid range.
---@param min number? Defaults to current.
---@param max number? Defaults to current.
---@param step number? Defaults to current.
function Spinner:SetBounds(min, max, step)

---@param width number
---@param height number
function Spinner:SetSize(width, height)

```
```lua
---@class GenericUI_Prefab_Text

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param text string
---@param alignType GenericUI_Element_Text_Align
---@param size Vector2
---@return GenericUI_Prefab_Text 
function Text.Create(ui, id, parent, text, alignType, size)

---@param text string
function Text:SetText(text)

function Text:GetMainElement()

```
```lua
---@class GenericUI_Prefab_FormHorizontalList

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param label string
---@param size Vector2
---@param labelSize Vector2
---@return GenericUI_Prefab_FormHorizontalList 
function Form.Create(ui, id, parent, label, size, labelSize)

---@param id string
---@param type `T`|GenericUI_ElementType
---@return `T` 
function Form:AddChild(id, type)

```
```lua
---@class GenericUI_Prefab_LabelledIcon

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param icon string
---@param text string
---@param iconSize Vector2
---@param textSize Vector2
---@return GenericUI_Prefab_LabelledIcon 
function Icon.Create(ui, id, parent, icon, text, iconSize, textSize)

```
```lua
---@class GenericUI_Prefab_Status
---@field EntityHandle EntityHandle
---@field StatusHandle EntityHandle
---@field Background GenericUI_Element_TiledBackground
---@field Icon GenericUI_Element_IggyIcon
---@field DurationText GenericUI_Prefab_Text
---@field BorderDummy GenericUI_Element_Empty

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param entity EclCharacter|EclItem
---@param status EclStatus
---@return GenericUI_Prefab_Status 
function Status.Create(ui, id, parent, entity, status)

---@param entity EclCharacter|EclItem
---@param status EclStatus
function Status:SetStatus(entity, status)

```
```lua
---@class GenericUI_Prefab_TooltipPanel
---@field Background GenericUI_Element_TiledBackground
---@field HeaderText GenericUI_Element_Text

---Creates a tooltip panel.
---@param ui GenericUI_Instance
---@param id string
---@param size Vector2
---@param parent (GenericUI_Element|string)?
---@param header string
---@param headerSize Vector2
---@return GenericUI_Prefab_TooltipPanel 
function TooltipPanelPrefab.Create(ui, id, parent, size, header, headerSize)

---@param id string
---@param elementType `T`|GenericUI_ElementType
---@return `T` 
function TooltipPanelPrefab:AddChild(id, elementType)

function TooltipPanelPrefab:Destroy()

```
```lua
---@class GenericUI_Prefab_FormElementBackground
---@field Background GenericUI_Element_TiledBackground
---@field HorizontalList GenericUI_Element_HorizontalList

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param size Vector2
---@return GenericUI_Prefab_FormElementBackground 
function BG.Create(ui, id, parent, size)

```
```lua
---Base class for prefabs styled as a form element.
---@class GenericUI_Prefab_FormElement
---@field Background GenericUI_Element_TiledBackground
---@field Label GenericUI_Prefab_Text

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param size Vector2
---@return GenericUI_Prefab_FormElement 
function Prefab.Create(ui, id, parent, size)

---@return GenericUI_Element_TiledBackground 
function Prefab:GetRootElement()

---Sets the size of the background.
---@param size Vector2
function Prefab:SetBackgroundSize(size)

---Returns the label of the element.
---@return string 
function Prefab:GetLabel()

---Sets the label.
---@param label string
function Prefab:SetLabel(label)

---Sets whether the element should be centered in lists.
---@param center boolean
function Prefab:SetCenterInLists(center)

---Sets the tooltip of the element.
---@param type TooltipLib_TooltipType
---@param tooltip any TODO document
function Prefab:SetTooltip(type, tooltip)

```
```lua
---@class GenericUI_Prefab_LabelledCheckbox
---@field Checkbox GenericUI_Element_StateButton
---@field _Style "Right-aligned"|"Left-aligned"

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param label string
---@param size Vector2? Defaults to `DEFAULT_SIZE`
---@return GenericUI_Prefab_LabelledCheckbox 
function Checkbox.Create(ui, id, parent, label, size)

---@param active boolean
function Checkbox:SetState(active)

---@param width number
---@param height number
function Checkbox:SetSize(width, height)

---Changes the layout of the element.
---@param style "Right-aligned"|"Left-aligned" Default style is `"Right-aligned"`
function Checkbox:SetStyle(style)

---Re-renders the element with the current style.
function Checkbox:Render()

```
```lua
---@class GenericUI_Prefab_LabelledSlider
---@field Slider GenericUI_Element_Slider
---@field LeftValueLabel GenericUI_Prefab_Text
---@field RightValueLabel GenericUI_Prefab_Text
---@field CurrentValueLabel GenericUI_Prefab_Text

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param size Vector2
---@param label string
---@param min number
---@param max number
---@param step number
---@return GenericUI_Prefab_LabelledSlider 
function Slider.Create(ui, id, parent, size, label, min, max, step)

---Sets the minimum value allowed on the slider.
---@param min number
function Slider:SetMin(min)

---Sets the maximum value allowed on the slider.
---@param max number
function Slider:SetMax(max)

---Sets the value of the slider.
---@param value number
function Slider:SetValue(value)

```
```lua
---@class GenericUI_Prefab_LabelledDropdown
---@field ComboBox GenericUI_Element_ComboBox

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param label string
---@param opts GenericUI_Element_ComboBox_Option[]?
---@param size Vector2? Defaults to `DEFAULT_SIZE`
---@return GenericUI_Prefab_LabelledDropdown 
function Dropdown.Create(ui, id, parent, label, opts, size)

---@param width number
---@param height number
function Dropdown:SetSize(width, height)

---@param id string
function Dropdown:SelectOption(id)

```
```lua
---@class GenericUI_Prefab_LabelledTextField
---@field Text GenericUI_Prefab_Text

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param label string
---@param size Vector2? Defaults to `DEFAULT_SIZE`
---@return GenericUI_Prefab_LabelledTextField 
function Text.Create(ui, id, parent, label, size)

---@param width number
---@param height number
function Text:SetSize(width, height)

---@param text string
function Text:SetText(text)

```
```lua
---@class GenericUI_Prefab_FormSetEntry
---@field RemoveButton GenericUI_Element_Button

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param label string
---@param minimumSize Vector2
---@return GenericUI_Prefab_FormSetEntry 
function Prefab.Create(ui, id, parent, label, minimumSize)

```
```lua
---@class GenericUI_Prefab_FormSet
---@field HorizontalList GenericUI_Element_HorizontalList
---@field AddButton GenericUI_Element_Button
---@field _MinimumSize Vector2

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param label string
---@param minimumSize Vector2
---@return GenericUI_Prefab_FormSet 
function Prefab.Create(ui, id, parent, label, minimumSize)

---@param setting SettingsLib_Setting_Set
function Prefab:RenderFromSetting(setting)

```
```lua
---@class GenericUI_Prefab_Selector
---@field ScrollLeftButton GenericUI_Element_Button
---@field ScrollRightButton GenericUI_Element_Button
---@field SubElementsLists GenericUI_Element_VerticalList[]
---@field Options string[]
---@field _CurrentOptionIndex integer
---@field _SelectorLabel string

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param label string
---@param size Vector2? Defaults to `DEFAULT_SIZE`
---@param options string[]
---@return GenericUI_Prefab_Selector 
function Selector.Create(ui, id, parent, label, size, options)

---Returns the container for subelements of an option's index.
---@param index integer
---@return GenericUI_Element_VerticalList 
function Selector:GetSubElementContainer(index)

---Changes the selector's value to the previous or next one.
---@param direction "Left"|"Right"
function Selector:Scroll(direction)

---Sets the selected option.
---@param index integer
function Selector:SetSelectedOption(index)

function Selector:SetBackgroundSize(size)

```
```lua
---@class GenericUI_Prefab_Bedazzled_Gem
---@field Gem Feature_Bedazzled_Board_Gem
---@field Root GenericUI_Element_Empty
---@field Icon GenericUI_Element_IggyIcon

---@param ui GenericUI_Instance
---@param id string
---@param parent (GenericUI_Element|string)?
---@param gem Feature_Bedazzled_Board_Gem
---@return GenericUI_Prefab_Bedazzled_Gem 
function GemPrefab.Create(ui, id, parent, gem)

---@param tween GenericUI_ElementTween
function GemPrefab:Tween(tween)

function GemPrefab:Update()

---Gets the icon for a modified gem.
---@param gemType string
---@param modifier string
---@return icon 
function GemPrefab.GetIconForModifier(gemType, modifier)

function GemPrefab:UpdateIcon()

---Returns the gem's position on the UI grid, in pixels.
function GemPrefab:GetGridPosition()

function GemPrefab:Destroy()

```
</doc>

## Events

<doc class="GenericUI" symbols="Listenable">

```lua
---@event Button_Pressed
---@field RegisterListener fun(self, listener:fun(stringID:string))
---@field Fire fun(self, stringID:string)

---@event StateButton_StateChanged
---@field RegisterListener fun(self, listener:fun(stringID:string, active:boolean))
---@field Fire fun(self, stringID:string, active:boolean)

---@event ViewportChanged
---@field Width integer
---@field Height integer

```
</doc>

## Methods

<doc class="GenericUI" symbols="Function">

```lua
```
</doc>