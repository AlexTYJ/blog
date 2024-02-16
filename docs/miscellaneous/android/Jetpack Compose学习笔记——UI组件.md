# Jetpack Compose学习笔记——UI组件

## Modifier

执行顺序：Modifer.first().second()

| **操作符**                | **参数**             | **示例**                                                      |
| ------------------------- | -------------------- | ------------------------------------------------------------- |
| **.size**                 | width,height         |                                                               |
|                           | size                 |                                                               |
| **.width**                | width                |                                                               |
| **.clip**                 | shape                | CircleShape,RoundedCornerShape(size)                          |
| **.background**           | color,shape          | Color.Red/Color(color) //ARGB                                 |
| **.height**               | height               |                                                               |
|                           | brush                | Brush.verticalGradient(colors=listof(Color.Red,Color.Yellow)) |
| **.align***               | alignment            | Alignment.Center                                              |
| **.fillMaxSize***         |                      |                                                               |
| **.fillMaxHeight***       |                      |                                                               |
| **.fillMaxWidth***        |                      |                                                               |
| **.border**               | width,color,shape    |                                                               |
|                           | brush                |                                                               |
| **.padding**              | all                  |                                                               |
|                           | horizontal,vertical  |                                                               |
|                           | top,bottom,start,end |                                                               |
| **.offset**               | x,y                  |                                                               |
| **.matchParentSize\*(B)** |                      |                                                               |
| **.fillMaxSize**          |                      |                                                               |
| **.fillMaxHeight**        |                      |                                                               |
| **.fillMaxWidth**         |                      |                                                               |
| **.wight\*(R/C)**         | wight                | 1f                                                            |

## 基础组件

### 文字组件

| 组件                   | 常用参数                                                                                    | 示例                                                                                                                                     |
| ---------------------- | ------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Text**               | text,style,color,maxLines,overflow                                                          | text=stringResourcde(R.string.xx)/"xxx"                                                                                                  |
|                        |                                                                                             | style=TextStyle(fontSize,letterSpacing,fontFamily,fontWeight)                                                                            |
|                        |                                                                                             | overflow=TextOverflow.Ellipsis                                                                                                           |
|                        |                                                                                             | text=buildAnnotatedString{withStyle(style=SpanStyle/ParagraphStyle()){append("")}}                                                       |
|                        | textDecoration                                                                              | textDecoration=TextDecoration.Underline                                                                                                  |
| **ClickableText**      | onclick:(offset) -> Unit                                                                    | onclick={offset->annotatedText.getStringAnnotations(tag="",start=offset,end=offset).firstOrNull()?.let{annotation->xx(annotation.item)}} |
| **SelectionContainer** |                                                                                             | SelectionContainer{Text()}                                                                                                               |
| **TextField**          | value,onValueChange:(value)->Unit,label:@Composable()->Unit                                 | value=text,onValueChange={text=it},label={Text()}                                                                                        |
|                        | leadingIcon,tailingIcon:@Composable()->Unit                                                 |                                                                                                                                          |
| **OutlinedTextField**  | value,onValueChange:(value)->Unit,label:@Composable()->Unit,placeholder:@Composable()->Unit |                                                                                                                                          |
| **BasicTextField**     | value,onValueChange:(value)->Unit                                                           |                                                                                                                                          |
|                        | decorationBox:@Composable(innerTextField)->Unit                                             | decorationBox={innerTextField->Box{if(text.isEmpty(){Text()}innerTextFiled()}                                                            |

### 图片组件

| 组件      | 常用参数                                          | 示例                                                                                     |
| --------- | ------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Icon**  | contentDescription,tint                           |                                                                                          |
|           | imageVector:ImageVector                           | imageVector=ImageVector.vectorResource(id=R.drawable.xxx)                                |
|           | bitmap:ImageBitmap                                | bitmap=ImageBitmap.imageResource(id=R.drawable.xxx)                                      |
|           | **painter:Painter**                               | painter=PainterResource(id=R.drawable.xxx)                                               |
|           |                                                   | Icons.Filled.Favorite                                                                    |
| **Image** | painter,contentDescription,alignment,contentScale | contentScale=ContentScale.Crop(居中裁剪)/Fit/FillHeight/FillWidth/Inside/None/FillBounds |
|           | colorFilter                                       |                                                                                          |

### 按钮组件

| 组件                             | 常用参数                                                           | 示例                                                                               |
| -------------------------------- | ------------------------------------------------------------------ | ---------------------------------------------------------------------------------- |
| **Button**                       | onClick:()->Unit,colors                                            | Button(colors=ButtonDefaults.buttonColors(backgroundColor = xx)){Text()//rowScope} |
| **IconButton**                   | onClick:()->Unit                                                   | IconButton(onclick={}){Icon()}                                                     |
| **FloatingActionButton**         | onClick:()->Unit                                                   | FloatingActionButton(onclick={}){Icon()}                                           |
| **ExtendedFloatingActionButton** | onClick:()->Unit,icon:@Composable()->Unit,text:@Composable()->Unit |                                                                                    |

### 选择器

| 组件                 | 常用参数                                                         | 示例                                                   |
| -------------------- | ---------------------------------------------------------------- | ------------------------------------------------------ |
| **Checkbox**         | checked,onCheckedChange:(Boolean)->Unit,colors                   | colors=CheckboxDefaults.colors(     checkmarkColor=xx) |
| **TriStateCheckBox** | state,onclick,colors                                             | state=ToggleableState.On/Off/Indeterminate             |
| **Switch**           | checked,onCheckedChange:(Boolean)->Unit,colors                   |                                                        |
| **Slider**           | value,onvalueChange:(Float)->Unit,steps,colors,valueRange=0f..1f |                                                        |

### 对话框

| 组件                          | 常用参数                                                                                                                                           | 示例                                                                                                                            |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Dialog**                    | onDismissResqueset:()->Unit,properties                                                                                                             | properties=DialogProperties(usePlatformDefaultWidth=false)                                                                      |
| **AlertDialog**               | onDismissResqueset:()->Unit,title:@Composable()->Unit,text:@Composable()->Unit,confirmButton:@Composable()->Unit,dismissButton:@Composable()->Unit |                                                                                                                                 |
| **CircularProgressIndicator** | progress                                                                                                                                           | val animatedProgress by animateFloatAsState(targetValue=progress,animationSpec=ProgressIndicatorDefaults.ProgressAnimationSpec) |
| **LinearProgressIndicator**   | progress                                                                                                                                           |                                                                                                                                 |

## 布局组件

### 线性布局

| 布局       | 常用参数                                          | 示例                                                  |
| ---------- | ------------------------------------------------- | ----------------------------------------------------- |
| **Column** | vecticalArrangement,horizontalAlignment           | Aligment.Start                                        |
|            | Modifier.fillMaxSize().background(xx).padding(xx) |                                                       |
| **Row**    | vecticalAlignment,horizontalArrangement           | Arrangement.Center/Start/End/SpaceBetween/SpaceEvenly |

### 帧布局

| 布局                      | 常用参数                              |
| ------------------------- | ------------------------------------- |
| **Box**                   | contentAlignment                      |
|                           | Modifier.fillMaxWidth().height(32.dp) |
| **Surface**(解耦Modifier) | shape,elevation                       |
| **Card**                  | shape,elevation                       |

### Spacer留白

**Spacer**(modifier=Modifier.width().height())

### 约束布局

**创建和绑定引用:**

```kotlin
val imageRef = remember {createRef()}
val (imageRef, textRef) = remember {createRefs()}

modifer = Modifier.constrainAs(imageRef) {
    top.linkTo(parent.top)
    start.linkTo(textRef.end, 10.dp)
    width = Dimension.preferredWrapContent
}
```

| 约束          | 创建                                                                            |
| ------------- | ------------------------------------------------------------------------------- |
| **Barrier**   | createEndBarrier(ref1,ref2)                                                     |
| **Guildline** | createGuidelineFromTop(weight:Float)                                            |
| **Chain**     | createVerticalChain(ref1,ref2,chainStyle=ChainStyle.Spread/SpreadInside/Packed) |

### Scaffold脚手架

```kotlin
val scaffoldState = rememberScaffoldState()
val scope = rememberCoroutineScope()

Scaffold(
	topBar = {
        TopAppBar(
        	title = {
                Text("")
            },
            navigationIcon = {
                IconButton(
                	onClick = { }
                ) {
                    Icon(...)
                }
            }
        )
    },
    bottomBar = {
        ButtonNavigation {
            items.forEachIndexed {index, item ->
        		ButtomNavigationItem(
                	selected = ..,
                    onClick = { },
                    icon = {Icon(..)},
                    alwaysShowLabel = ..,
                    label = {Text(..)}
                )
        	}
        }
    },
    drawerContent = {
        
    },
    scaffoldState = scaffoldState
) {
    
}
BackHandler(
	enabled = scaffoldState.drawerState.isOpen
) {
    scope.launch {
        scaffoldState.drawerState.close()
    }
}
```

## 列表

### DropdownMenu

```kotlin
DropdownMenu(
	expanded = ..,
	onDismissResquest = ..	
) {
    Column {
        options.forEach {option ->
        	ListItem(text = {Text("")})
        }
    }
}
```

### LazyComposables

```kotlin
LazyColumn(
	contentPadding = PaddingValues(35.dp),
	verticalArrangement = Arrangement.spaceBy(10.dp)
) {
	item {
		Text("")
	}
	items(5) { index ->
		...
	}
	items(List<T>) { option ->
		...
	}
	
}
```

