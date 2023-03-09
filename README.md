### Rider 使用 IdeaVim 编辑使用.
工具: [Rider](https://www.jetbrains.com/rider/) + [IdeaVim](https://plugins.jetbrains.com/plugin/164-ideavim) + [IdeaVim-Sneak](https://plugins.jetbrains.com/plugin/15348-ideavim-sneak) + [IdeaVimExtension](https://plugins.jetbrains.com/plugin/9615-ideavimextension) + [IdeaVim-Quickscope](https://plugins.jetbrains.com/plugin/19417-ideavim-quickscope) + [AutoHotKey](https://www.autohotkey.com/)
这里将使用 IdeaVim 在 Rider 中进行 C# 编程开发,这些规则同样适用于 JetBrains 的其它 IDE 工具(GoLand).
vim 强大的能力来自一系列的组合, Rider 本身作为 IDE 也提供很多特性，在 Rider 中使用 vim 会带来更多的可能性.这里期望通过文章来展示一些在 Rider 中使用 IdeaVim 的技巧.


### 设置
这里是一些个性化的设置，默认的一些设置符合大多数人，但是也会根据自身的需求进行适当调整.

#### Rider
Rider 在屏幕上存在大量鼠标访问 UI 元素，对于使用键盘编程来说这些东西是不需要的。尽量使用键盘而非鼠标，并且其中都是可以通过键盘进行访问，所以这里进行一些调整将 UI 元素都进行隐藏.
1. 全屏模式(View -> Appearance -> Enter Full Sceen or Alt+Shift+Enter)
2. 将 breadcrums 由底部调整为顶部(File -> Settings -> Editor -> General -> Breadcrumbs -> Placement: Top)
3. 关闭 Main Menu(View -> Appearance -> Main Menu)
4. 关闭 Toolbar(View -> Appearance -> Toolbar)
5. 关闭 Navigation bar(View -> Appearance -> Navigation bar)
6. 关闭 Status Bar(View -> Appearance -> Status Bar)
7. 关闭 Navigation bar(View -> Appearance -> Navigation bar)
8. 关闭 Tool Window Bars(View -> Appearance -> Tool Windows Bars)


#### idaevimrc
在这个文件中，我们可以定义命令，不仅仅包含 vim 的原生的命令，也可以调用 Rider 提供的一系列命令,如下是一些配置信息
```
" M->Alt, A->Win, C->control
" <ESC> - escape, <BS> - backspace, <CR> - return

" 使用空格作为 leader 键
let mapleader = " "

" ------------------------------------- Plugins ------------------------------
" 开启 NERDTree 插件
set NERDTree
nnoremap <leader>e :NERDTreeToggle <CR>

set ReplaceWithRegister
set argtextobj
set exchange
set highlightedyank
set surround

set easymotion
map s <Plug>(easymotion-bd-f2)
map S <Plug>(easymotion-bd-w)

set textobj-indent
set commentary

" dependent on IdeaVim-Quickscope Plugin
set quickscope
let g:qs_highlight_on_keys = ['f', 'F', 't', 'T']


" dependent on IdeaVimExtension Plugin
set keep-english-in-normal

""" Idea specific settings ------------------
set ideajoin
set ideastatusicon=gray
" set idearefactormode=visual

" ------------------------------------ Common ----------------------
set hlsearch
set incsearch
set ignorecase 
set smartcase
set scrolloff=5
set showmode
set showcmd
set history=10000
set number 
set wrapscan
set clipboard=unnamed,unnamedplus
set clipboard+=ideaput
set timeout
set timeoutlen=300

" ------------------------------------- Debug -------------------------------
map <leader>db <action>(ToggleLineBreakpoint)
map <leader>dc <action>(Resume)
map <leader>di <action>(StepInto)
map <leader>do <action>(StepOver)
map <leader>dO <action>(StepOut)
map <leader>dl <action>(Rerun)
map <leader>de <action>(ViewBreakpoints)
map <leader>da <action>(XDebugger.AttachToProcess)

" -------------------------------------- Run --------------------------------
map <leader>du <action>(Debug)
map <leader>c <action>(Stop)
map <leader>ru <action>(Run)
map <leader>b <action>(BuildSolutionAction)
map <leader>rb <action>(RebuildSolutionAction)

" -------------------------------------- Code --------------------------------
nnoremap [<space> O<esc>j
nnoremap ]<space> o<esc>k
nmap == <action>(ReformatCode)
vmap == <action>(ReformatCode)

" -------------------------------------- Views --------------------------------
map <leader>z <action>(ToggleZenMode)
map <leader>fw <action>(ToggleFullScreen)

" -------------------------------------- Refactoring --------------------------------
map <leader>cs <action>(ChangeSignature)
map <leader>rn <action>(RenameElement)
map <leader>sd <action>(SafeDelete)
map <leader>iv <action>(IntroduceVariable)
map <leader>em <action>(ExtractMethod)

" -------------------------------------- Generate --------------------------------
map <leader>im <action>(ImplementMethods)
map <leader>om <action>(OverrideMethods)
map <leader>cg <action>(Generate)

" -------------------------------------- Jump --------------------------------
map <c-i> <action>(Forward)
map <c-o> <action>(Back)
map g, <action>(JumpToNextChange)
map g; <action>(JumpToLastChange)
map gb <action>(GotoSuperMethod)
map gi <action>(GotoImplementation)
map gd <action>(GotoDeclaration)
map gD <action>(GotoTypeDeclaration)
map gj <action>(MethodDown)
map gk <action>(MethodUp)
map <leader>ge <action>(GotoNextError)
map <leader>gE <action>(GotoPreviousError)

" -------------------------------------- Search --------------------------------
map <c-p> <action>(GotoFile)
map <c-n> <action>(RecentFiles)
map <leader>ga <action>(GotoAction)
map <leader>gc <action>(GotoClass)
map <leader>gs <action>(GotoSymbol)
map <leader>ge <action>(SearchEverywhere)
map <leader>fm <action>(FileStructurePopup)
map <leader>ft <action>(FindInPath)
map <leader>vo <action>(RiderShowValueOrigin)
map <leader>vd <action>(RiderShowValueDestination)
map <leader>ci <action>(RiderShowIncomingCalls)
map <leader>co <action>(RiderShowOutgoingCalls)

" -------------------------------------- Window --------------------------------
map <leader>ha <action>(HideAllWindows)

" -------------------------------------- Information --------------------------------
map <leader>jd <action>(QuickJavaDoc)
map <leader>se <action>(ShowErrorDescription)
map <leader>qm <action>(QuickImplementations)
map <leader>fu <action>(FindUsages)
map <leader>su <action>(ShowUsages)

" -------------------------------------- Utilities --------------------------------
map <leader>w :w <CR>
map Y y$
map <leader>y yiw
map <leader>p viw"0p
map <C-h> <Action>(TypeHierarchy)
map <leader>a <action>(Annotate)
map <leader>s <action>(SelectInProjectView)
```

#### Auto Hot Key

