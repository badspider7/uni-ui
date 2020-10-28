发现错误？想参与编辑？[在 GitHub 上编辑此页面！](https://github.com/dcloudio/uni-ui/blob/master/src/components/uni-list/readme.md)
## List 列表
> 组件名：``uni-list``、``uni-list-item``，代码块： uList、uListItem。

List 列表组件，包含基本列表样式、可扩展插槽机制、长列表性能优化、多端兼容。

在vue页面里，它默认使用页面级滚动。在app-nvue页面里，它默认使用原生list组件滚动。这样的长列表，在滚动出屏幕外后，系统会回收不可见区域的渲染内存资源，不会造成滚动越长手机越卡的问题。

uni-list组件是父容器，里面的核心是uni-list-item子组件，它代表列表中的一个可重复行，子组件可以无限循环。

uni-list-item有很多风格，uni-list-item组件通过内置的属性，满足一些常用的场景。当内置属性不满足需求时，可以通过扩展插槽来自定义列表内容。

内置属性可以覆盖的场景包括：导航列表、设置列表、小图标列表、通信录列表、聊天记录列表。

涉及很多大图或丰富内容的列表，比如类今日头条的新闻列表、类淘宝的电商列表，需要通过扩展插槽实现。

下文均有样例给出。

uni-list不包含下拉刷新和上拉翻页。上拉翻页另见组件：[uni-load-more](https://ext.dcloud.net.cn/plugin?id=29)

### 平台差异说明

如无特殊说明，则全平台支持

### 组件使用注意事项

为了避免错误使用，给大家带来不好的开发体验，请在使用组件前仔细阅读下面的注意事项，可以帮你避免一些必要的错误使用。

- 组件需要依赖 `sass` 插件 ，请自行手动安装
- 组件内部依赖 `'uni-icons'` 、`uni-badge` 组件
- `uni-list` 和 `uni-list-item` 需要配套使用，暂不支持单独使用 `uni-list-item`
- 只有开启点击反馈后，会有点击选中效果
- 使用插槽时，可以完全自定义内容
- note 、rightText 属性暂时没做限制，不支持文字溢出隐藏，使用时应该控制长度显示或通过默认插槽自行扩展
- 支付宝小程序平台需要在支付宝小程序开发者工具里开启 component2 编译模式，开启方式： 详情 --> 项目配置 --> 启用 component2 编译
- 如果需要修改 `switch`、`badge` 样式，请使用插槽自定义
- 在 `HBuilderX` 低版本中，可能会出现组件显示 `undefined` 的问题，请升级最新的 `HBuilderX` 或者 `cli`
- 如使用过程中有任何问题，或者您对uni-ui有一些好的建议，欢迎加入 uni-ui 交流群：871950839

### 如何在项目中引用uni-list组件

#### 方式1 (推荐)

`HBuilderX 2.5.5`起支持 `easycom` 组件模式。在使用 `uni-ui` 的时候，只要[uni-ui组件](https://ext.dcloud.net.cn/plugin?id=55) 安装在项目的 `components` 目录下,并符合 `components/组件名称/组件名称.vue` 目录结构。就可以不用引用、注册，直接在页面中使用 `uni-ui` 组件

`easycom` 组件模式的好处在于不管 `components` 目录下安装了多少组件，`easycom` 打包后会自动剔除没有使用的组件，对组件库的使用尤为友好,组件库批量安装，随意使用，自动按需打包。 关于 `easycom` 更详细内容 [参考文档](https://uniapp.dcloud.io/collocation/pages?id=easycom)

在HBuilderX中新建项目时，选择uni ui项目，创建的工程即带有所有uni ui组件。此时在页面里敲ulist代码块，回车，即可编写一个list组件。

#### 方式2（vue-cli）

**初始化项目**

如果是使用 `HBuiderX` 创建的项目，需先执行以下命令初始化：

```
npm init -y
```

**安装 uni-ui**

```
npm install @dcloudio/uni-ui -D
```


在 ``script`` 中引用组件：

```javascript
import {uniList,uniListItem,uniListChat} from '@dcloudio/uni-ui'
export default {
    components: {uniPopup,uniListItem,uniListChat}
}
```

#### 方式3（vue-cli + easycom）

使用 `方式2` 安装好 `uni-ui` 之后，需要配置 `easycom` 规则，让 `npm` 安装的组件支持  `easycom`

打开项目根目录下的 `pages.json` 并添加 `easycom` 节点：

```javascript
// pages.json

{
	"easycom": {
		"autoscan": true,
		"custom": {
			// uni-ui 规则如下配置
			"^uni-(.*)": "@dcloudio/uni-ui/lib/uni-$1/uni-$1.vue"
		}
	},
	
	// 其他内容
	pages:[
		// ...
	]
}

```



### 基本用法 

```html
<!-- 单行内容显示 -->
<uni-list>
	<uni-list-item  title="列表文字" ></uni-list-item>
	<uni-list-item :disabled="true" title="列表禁用状态" ></uni-list-item>
</uni-list>
<!-- 多行内容显示 -->
<uni-list>
	<uni-list-item title="列表文字" note="列表描述信息"></uni-list-item>
	<uni-list-item :disabled="true" title="列表文字" note="列表禁用状态"></uni-list-item>
</uni-list>
<!-- 右侧显示角标、switch -->
<uni-list>
	<uni-list-item  title="列表右侧显示角标" :show-badge="true" badge-text="12" ></uni-list-item>
	<uni-list-item title="列表右侧显示 switch"  :show-switch="true"  @switchChange="switchChange" ></uni-list-item>
</uni-list>
 <!-- 左侧显示略缩图、图标 -->
 <uni-list>
 	<uni-list-item title="列表左侧带略缩图" note="列表描述信息" thumb="https://img-cdn-qiniu.dcloud.net.cn/new-page/uni.png"
 	 thumb-size="lg" rightText="右侧文字"></uni-list-item>
 	<uni-list-item :show-extra-icon="true" :extra-icon="extraIcon1" title="列表左侧带扩展图标" ></uni-list-item>
</uni-list>
			 
```

### 开启点击反馈和右侧箭头
- 设置 `clickable` 为 `true` ，则表示这是一个可点击的列表，会默认给一个点击效果，并可以监听 `click` 事件
- 设置 `link` 属性，会自动开启点击反馈，并给列表右侧添加一个箭头
- 设置 `to` 属性，可以跳转页面，`link` 的值表示跳转方式，如果不指定，默认为 `navigateTo`

```html

<uni-list>
	<uni-list-item title="开启点击反馈" clickable  @click="onClick" ></uni-list-item>
	<uni-list-item title="默认 navigateTo 方式跳转页面" link to="/pages/vue/index/index" @click="onClick($event,1)" ></uni-list-item>
	<uni-list-item title="reLaunch 方式跳转页面" link="reLaunch" to="/pages/vue/index/index" @click="onClick($event,1)" ></uni-list-item>
</uni-list>

```



### uni-list 属性说明
列表组件的父组件，所有列表组件都需要放到 uni-list 中，才能正常显示

**uniList 属性说明：**

属性名			|类型		|默认值		|	说明																									
---				|----		|---		|	---	
border			|Boolean	|true		|	是否显示边框


### uni-list-item 属性说明

uni-list-item的内置属性，可以覆盖的场景包括：导航列表、设置列表、小图标列表、通信录列表、聊天记录列表。更多场景比如复杂的图文列表，可通过扩展插槽实现。

**uniListItem 属性说明：**

属性名			|类型		|默认值		|	说明																					
---				|----		|---		|	---	
title			|String		|-			|	标题
note			|String		|-			|	描述
ellipsis		|Number		|0			|	title 是否溢出隐藏，可选值，0:默认;  1:显示一行;	2:显示两行;【nvue 暂不支持】
thumb			|String		|-			|	左侧缩略图，若thumb有值，则不会显示扩展图标
thumbSize		|String 	|medium 	|	略缩图尺寸，可选值，lg:大图;  medium:一般;	sm:小图;
showBadge		|Boolean	|false		|	是否显示数字角标	
badgeText		|String		|-			|	数字角标内容
badgeType		|String		|-			|	数字角标类型，参考[uni-icons](https://ext.dcloud.net.cn/plugin?id=21)					
rightText		|String		|-			|	右侧文字内容
disabled		|Boolean	|false		|	是否禁用	
showArrow 		|Boolean	|true		|	是否显示箭头图标			
link			|String 	|navigateTo	|	新页面跳转方式，可选值见下表
to				|String		|-			|	新页面跳转地址，如填写此属性，click 会返回页面是否跳转成功			
clickable		|Boolean	|false		|	是否开启点击反馈
showSwitch	    |Boolean	|false		|	是否显示Switch																			
switchChecked	|Boolean	|false		|	Switch是否被选中																			
showExtraIcon   |Boolean	|false		|	左侧是否显示扩展图标																		
extraIcon		|Object		|-			|	扩展图标参数，格式为 ``{color: '#4cd964',size: '22',type: 'spinner'}``，参考 [uni-icons](https://ext.dcloud.net.cn/plugin?id=28)	
direction		| String	|row		|	排版方向，可选值，row:水平排列;  column:垂直排列; 3个插槽是水平排还是垂直排，也受此属性控制


**link 属性说明：**

属性名		|	说明
---			|	---
navigateTo 	| 	同 uni.navigateTo()
redirectTo 	|	同 uni.reLaunch()
reLaunch	|	同 uni.reLaunch()
switchTab  	|	同 uni.switchTab()


### uni-list-item 插槽说明
> 注意：与之前的插槽不兼容，left 更改为 header ， right 更改为 footer

如果	`uni-list-item` 组件内置属性样式无法满足需求，可以使用插槽来自定义uni-list-item里的内容。

uni-list-item提供了3个可扩展的插槽：`header`、`body`、`footer`

- 当 `direction` 属性为 `row` 时表示水平排列，此时 `header` 表示列表的左边部分，`body` 表示列表的中间部分，`footer` 表示列表的右边部分
- 当 `direction` 属性为 `column` 时表示垂直排列，此时 `header` 表示列表的上边部分，`body` 表示列表的中间部分，`footer` 表示列表的下边部分

开发者可以只用1个插槽，也可以3个一起使用。在插槽中可自主编写view标签，实现自己所需的效果。

**Tips**

需要注意的是当使用插槽时，内置样式将会失效，只保留排版样式，此时的样式需要开发者自己实现

**插槽**

名称	 	|	说明					
:-		|	:-						
header	|	左/上内容插槽，可完全自定义默认显示
body	|	中间内容插槽，可完全自定义中间内容				
footer	|	右/下内容插槽，可完全自定义右侧内容		
	
**示例**

```html
<uni-list>
	<uni-list-item title="自定义右侧插槽" note="列表描述信息" link>
		<template slot="header">
			<image class="slot-image" src="/static/logo.png" mode="widthFix"></image>
		</template>
	</uni-list-item>
	<uni-list-item>
		<!-- 自定义 header -->
		<view slot="header" class="slot-box"><image class="slot-image" src="/static/logo.png" mode="widthFix"></image></view>
		<!-- 自定义 body -->
		<text slot="body" class="slot-box slot-text">自定义插槽</text>
		<!-- 自定义 footer-->
		<template slot="footer">
			<image class="slot-image" src="/static/logo.png" mode="widthFix"></image>
		</template>
	</uni-list-item>
</uni-list>
```


**uniListItem 事件说明：**

事件称名			|说明									|返回参数			
---				|---									|---				
click			|点击 uniListItem 触发事件，需开启点击反馈	|-					
switchChange	|点击切换 Switch 时触发，需显示 switch		|e={value:checked}	

### 聊天列表

#### uni-list-chat 属性说明

用于聊天类型的列表展示，提供了基础角标、头像的展示

**uniListChat 属性说明：**

属性名			|类型		|默认值		|	说明																		
---				|----		|---		|	---	
title 			|String		|-			|	标题
note 			|String		|-			|	描述
clickable		|Boolean	|false		|	是否开启点击反馈
badgeText		|String		|-			|	数字角标内容，设置为 `dot` 将显示圆点
badgePositon 	|String		|right		|	角标位置
link			|String 	|navigateTo	|	是否展示右侧箭头并开启点击反馈，可选值见下表
clickable		|Boolean	|false		|	是否开启点击反馈
to				|String		|-			|	跳转页面地址，如填写此属性，click 会返回页面是否跳转成功	
time			|String 	|-			|	右侧时间显示
avatarCircle 	|Boolean 	|false		|	是否显示圆形头像
avatar			|String 	|-			|	头像地址，avatarCircle 不填时生效
avatarList 		|Array	 	|-			|	头像组，格式为 [{url:''}]


**link 属性说明：**

属性名		|	说明
---			|	---
navigateTo 	| 	同 uni.navigateTo()
redirectTo 	|	同 uni.reLaunch()
reLaunch	|	同 uni.reLaunch()
switchTab  	|	同 uni.switchTab()

#### 聊天列表示例
- 设置 `clickable` 为 `true` ，则表示这是一个可点击的列表，会默认给一个点击效果，并可以监听 `click` 事件
- 设置 `link` 属性，会自动开启点击反馈，`link` 的值表示跳转方式，如果不指定，默认为 `navigateTo`
- 设置 `to` 属性，可以跳转页面
- `time` 属性，通常会设置成时间显示，但是这个属性不仅仅可以设置时间，你可以传入任何文本，注意文本长度可能会影响显示
- `avatar` 和 `avatarList` 属性同时只会有一个生效，同时设置的话，`avatarList` 属性的长度大于1 ，`avatar` 属性将失效
- 可以通过默认插槽自定义列表右侧内容

```html

<uni-list>
	<uni-list :border="true">
		<!-- 显示圆形头像 -->
		<uni-list-chat :avatar-circle="true" title="uni-app" avatar="https://img-cdn-qiniu.dcloud.net.cn/new-page/uni.png" note="您收到一条新的消息" time="2020-02-02 20:20" ></uni-list-chat>
		<!-- 右侧带角标 -->
		<uni-list-chat title="uni-app" avatar="https://img-cdn-qiniu.dcloud.net.cn/new-page/uni.png" note="您收到一条新的消息" time="2020-02-02 20:20" badge-text="12"></uni-list-chat>
		<!-- 头像显示圆点 -->
		<uni-list-chat title="uni-app" avatar="https://img-cdn-qiniu.dcloud.net.cn/new-page/uni.png" note="您收到一条新的消息" time="2020-02-02 20:20" badge-positon="left" badge-text="dot"></uni-list-chat>
		<!-- 头像显示角标 -->
		<uni-list-chat title="uni-app" avatar="https://img-cdn-qiniu.dcloud.net.cn/new-page/uni.png" note="您收到一条新的消息" time="2020-02-02 20:20" badge-positon="left" badge-text="99"></uni-list-chat>
		<!-- 显示多头像 -->
		<uni-list-chat title="uni-app" :avatar-list="avatarList" note="您收到一条新的消息" time="2020-02-02 20:20" badge-positon="left" badge-text="dot"></uni-list-chat>
		<!-- 自定义右侧内容 -->
		<uni-list-chat title="uni-app" :avatar-list="avatarList" note="您收到一条新的消息" time="2020-02-02 20:20" badge-positon="left" badge-text="dot">
			<view class="chat-custom-right">
				<text class="chat-custom-text">刚刚</text>
				<!-- 需要使用 uni-icons 请自行引入 -->
				<uni-icons type="star-filled" color="#999" size="18"></uni-icons>
			</view>
		</uni-list-chat>
	</uni-list>
</uni-list>

```

```javascript

export default {
	components: {},
	data() {
		return {
			avatarList: [{
				url: 'https://img-cdn-qiniu.dcloud.net.cn/new-page/uni.png'
			}, {
				url: 'https://img-cdn-qiniu.dcloud.net.cn/new-page/uni.png'
			}, {
				url: 'https://img-cdn-qiniu.dcloud.net.cn/new-page/uni.png'
			}]
		}
	}
}

```


```css

.chat-custom-right {
	flex: 1;
	/* #ifndef APP-NVUE */
	display: flex;
	/* #endif */
	flex-direction: column;
	justify-content: space-between;
	align-items: flex-end;
}

.chat-custom-text {
	font-size: 12px;
	color: #999;
}

```


#### uni-list-chat 插槽说明

名称	 	|	说明					
:-		|	:-						
default	|	自定义列表右侧内容（包括时间和角标显示）

**uniListChat 事件说明：**

事件称名			|	说明						|	返回参数			
---				|	---						|	---	
@click			|	点击 uniListChat 触发事件	|	{data:{}}	，如有 to 属性，会返回页面跳转信息	

### uni-list插件预览地址

[https://uniapp.dcloud.io/h5/pages/extUI/list/list](https://uniapp.dcloud.io/h5/pages/extUI/list/list)

### 基于uni-list扩展的页面模板

通过扩展插槽，可实现多种常见样式的列表

**新闻列表类**

1. 云端一体混合布局：[https://ext.dcloud.net.cn/plugin?id=2546](https://ext.dcloud.net.cn/plugin?id=2546)
2. 云端一体垂直布局，大图模式：[https://ext.dcloud.net.cn/plugin?id=2583](https://ext.dcloud.net.cn/plugin?id=2583)
3. 云端一体垂直布局，多行图文混排：[https://ext.dcloud.net.cn/plugin?id=2584](https://ext.dcloud.net.cn/plugin?id=2584)
4. 云端一体垂直布局，多图模式：[https://ext.dcloud.net.cn/plugin?id=2585](https://ext.dcloud.net.cn/plugin?id=2585)
5. 云端一体水平布局，左图右文：[https://ext.dcloud.net.cn/plugin?id=2586](https://ext.dcloud.net.cn/plugin?id=2586)
6. 云端一体水平布局，左文右图：[https://ext.dcloud.net.cn/plugin?id=2587](https://ext.dcloud.net.cn/plugin?id=2587)
7. 云端一体垂直布局，无图模式，主标题+副标题：[https://ext.dcloud.net.cn/plugin?id=2588](https://ext.dcloud.net.cn/plugin?id=2588)

**商品列表类**

1. 云端一体列表/宫格视图互切：[https://ext.dcloud.net.cn/plugin?id=2651](https://ext.dcloud.net.cn/plugin?id=2651)
2. 云端一体列表（宫格模式）：[https://ext.dcloud.net.cn/plugin?id=2671](https://ext.dcloud.net.cn/plugin?id=2671)
3. 云端一体列表（列表模式）：[https://ext.dcloud.net.cn/plugin?id=2672](https://ext.dcloud.net.cn/plugin?id=2672)