---
ms.assetid: 4D47185C-8998-4903-AE64-7E2A67F9DF7A
title: UI 컨트롤 비교
description: 이 문서에서는 Xamarin.ios, Windows Forms 및 WPF 간의 UI 컨트롤을 비교 하 여 설명 합니다. 또한 WPF를 Xamarin.ios와 비교 하는 다른 설명서에 대 한 링크도 제공 합니다.
author: davidortinau
ms.author: daortin
ms.date: 04/26/2017
ms.openlocfilehash: b4cffd9e95f24dea9fc5fed5a6badeec624a4e25
ms.sourcegitcommit: 4e399f6fa72993b9580d41b93050be935544ffaa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91453092"
---
# <a name="ui-controls-comparison"></a>UI 컨트롤 비교

다음은 [이 테이블](/dotnet/framework/wpf/advanced/windows-forms-controls-and-equivalent-wpf-controls)을 기반으로 하는 WINDOWS FORMS 및 WPF와의 xamarin.ios 컨트롤 비교입니다.

모바일 앱 개발에 대 한 데스크톱 정보를 업데이트 하는 데 도움이 되는 [WPF와 xamarin.ios의 유사성 및 차이점](wpf.md) 에 대해 자세히 알아보세요.

|Windows Forms|WPF|Xamarin.Forms|
|--- |--- |--- |
|[BindingNavigator](/dotnet/api/system.windows.forms.bindingnavigator)|-|-|
|[BindingSource](/dotnet/api/system.windows.forms.bindingsource)|[CollectionViewSource](/dotnet/api/system.windows.data.collectionviewsource)|바인딩 속성 (예:) BindingContext|
|[Button](/dotnet/api/system.windows.forms.button)|[Button](/dotnet/api/system.windows.controls.button)|단추|
|[CheckBox](/dotnet/api/system.windows.forms.checkbox)|[CheckBox](/dotnet/api/system.windows.controls.checkbox)|스위치|
|[CheckedListBox](/dotnet/api/system.windows.forms.checkedlistbox)|컴퍼지션이 있는 [ListBox](/dotnet/api/system.windows.controls.listbox)|컴퍼지션이 있는 ListView.|
|[ColorDialog](/dotnet/api/system.windows.forms.colordialog)|-|-|
|[ComboBox](/dotnet/api/system.windows.forms.combobox)|[ComboBox](/dotnet/api/system.windows.controls.combobox) (자동 완성을 지원 하지 않음)|선택기|
|[ContextMenuStrip](/dotnet/api/system.windows.forms.contextmenustrip)|[ContextMenu](/dotnet/api/system.windows.controls.contextmenu)|-|
|[DataGridView](/dotnet/api/system.windows.forms.datagridview)|[DataGrid](/dotnet/api/system.windows.controls.datagrid)|-|
|[DateTimePicker](/dotnet/api/system.windows.forms.datetimepicker)|[DatePicker](/dotnet/api/system.windows.controls.datepicker)|DatePicker & TimePicker|
|[DomainUpDown](/dotnet/api/system.windows.forms.domainupdown)|[TextBox](/dotnet/api/system.windows.controls.textbox) 및 두 개의 [RepeatButton](/dotnet/api/system.windows.controls.primitives.repeatbutton) 컨트롤.|Stepper|
|[ErrorProvider](/dotnet/api/system.windows.forms.errorprovider)|-|-|
|[FlowLayoutPanel](/dotnet/api/system.windows.forms.flowlayoutpanel)|[WrapPanel](/dotnet/api/system.windows.controls.wrappanel) 또는 [StackPanel](/dotnet/api/system.windows.controls.stackpanel)|StackLayout 또는가는 레이아웃|
|[FolderBrowserDialog](/dotnet/api/system.windows.forms.folderbrowserdialog)|-|-|
|[FontDialog](/dotnet/api/system.windows.forms.fontdialog)|-|-|
|[Form](/dotnet/api/system.windows.forms.form)|[창](/dotnet/api/system.windows.window)|페이지|
|[GroupBox](/dotnet/api/system.windows.forms.groupbox)|[GroupBox](/dotnet/api/system.windows.controls.groupbox)|-|
|[HelpProvider](/dotnet/api/system.windows.forms.helpprovider)|해당 하는 컨트롤 (도구 설명 사용)이 없습니다.|-|
|[HScrollBar](/dotnet/api/system.windows.forms.hscrollbar)|[ScrollBar](/dotnet/api/system.windows.controls.primitives.scrollbar) (스크롤이 컨테이너 컨트롤에 기본 제공 됨)|ScrollView 사용|
|[ImageList](/dotnet/api/system.windows.forms.imagelist)|-|-|
|[레이블](/dotnet/api/system.windows.forms.label)|[레이블](/dotnet/api/system.windows.controls.label)|레이블|
|[LinkLabel](/dotnet/api/system.windows.forms.linklabel)|해당 하는 컨트롤이 없습니다. [Hyperlink](/dotnet/api/system.windows.documents.hyperlink) 클래스를 사용 하 여 유동 콘텐츠 내에서 하이퍼링크를 호스트할 수 있습니다.|-|
|[ListBox](/dotnet/api/system.windows.forms.listbox)|[ListBox](/dotnet/api/system.windows.controls.listbox)|ListView 사용|
|[ListView](/dotnet/api/system.windows.forms.listview)|[ListView](/dotnet/api/system.windows.controls.listview)|ListView|
|[MaskedTextBox](/dotnet/api/system.windows.forms.maskedtextbox)|-|-|
|[MenuStrip](/dotnet/api/system.windows.forms.menustrip)|[메뉴](/dotnet/api/system.windows.controls.menu)|MasterDetailPage 또는 TabbedPage 고려|
|[MonthCalendar](/dotnet/api/system.windows.forms.monthcalendar)|[캘린더](/dotnet/api/system.windows.controls.calendar)|-|
|[NotifyIcon](/dotnet/api/system.windows.forms.notifyicon)|-|-|
|[NumericUpDown](/dotnet/api/system.windows.forms.numericupdown)|[TextBox](/dotnet/api/system.windows.controls.textbox) 및 두 개의 [RepeatButton](/dotnet/api/system.windows.controls.primitives.repeatbutton) 컨트롤.|Stepper|
|[OpenFileDialog](/dotnet/api/system.windows.forms.openfiledialog)|[OpenFileDialog](/dotnet/api/microsoft.win32.openfiledialog)|-|
|[PageSetupDialog](/dotnet/api/system.windows.forms.pagesetupdialog)|-|-|
|[Panel](/dotnet/api/system.windows.forms.panel)|[캔버스](/dotnet/api/system.windows.controls.canvas)|보기 또는 AbsoluteLayout|
|[PictureBox](/dotnet/api/system.windows.forms.picturebox)|[이미지](/dotnet/api/system.windows.controls.image)|이미지|
|[PrintDialog](/dotnet/api/system.windows.forms.printdialog)|[PrintDialog](/dotnet/api/system.windows.controls.printdialog)|-|
|[PrintDocument](/dotnet/api/system.drawing.printing.printdocument)|-|-|
|[PrintPreviewControl](/dotnet/api/system.windows.forms.printpreviewcontrol)|[DocumentViewer](/dotnet/api/system.windows.controls.documentviewer)|-|
|[PrintPreviewDialog](/dotnet/api/system.windows.forms.printpreviewdialog)|-|-|
|[ProgressBar](/dotnet/api/system.windows.forms.progressbar)|[ProgressBar](/dotnet/api/system.windows.controls.progressbar)|ProgressBar|
|[PropertyGrid](/dotnet/api/system.windows.forms.propertygrid)|-|-|
|[RadioButton](/dotnet/api/system.windows.forms.radiobutton)|[RadioButton](/dotnet/api/system.windows.controls.radiobutton)|-|
|[RichTextBox](/dotnet/api/system.windows.forms.richtextbox)|[RichTextBox](/dotnet/api/system.windows.controls.richtextbox)|편집기에서 단일 줄 텍스트에 대 한 형식이 지정 된 서식 있는 텍스트를 지원 하지 않습니다.|
|[SaveFileDialog](/dotnet/api/system.windows.forms.savefiledialog)|[SaveFileDialog](/dotnet/api/microsoft.win32.savefiledialog)|-|
|[ScrollableControl](/dotnet/api/system.windows.forms.scrollablecontrol)|[ScrollViewer](/dotnet/api/system.windows.controls.scrollviewer)|ScrollView|
|[SoundPlayer](/dotnet/api/system.media.soundplayer)|[MediaPlayer](/dotnet/api/system.windows.media.mediaplayer)|-|
|[SplitContainer](/dotnet/api/system.windows.forms.splitcontainer)|[GridSplitter](/dotnet/api/system.windows.controls.gridsplitter)|MasterDetailPage 고려|
|[StatusStrip](/dotnet/api/system.windows.forms.statusstrip)|[StatusBar](/dotnet/api/system.windows.controls.primitives.statusbar)|-|
|[TabControl](/dotnet/api/system.windows.forms.tabcontrol)|[TabControl](/dotnet/api/system.windows.controls.tabcontrol)|TabbedPage|
|[TableLayoutPanel](/dotnet/api/system.windows.forms.tablelayoutpanel)|[그리드](/dotnet/api/system.windows.controls.grid)|그리드|
|[TextBox](/dotnet/api/system.windows.forms.textbox)|[TextBox](/dotnet/api/system.windows.controls.textbox)|편집기에서 서식 있는 서식 있는 텍스트를 지원 하지 않습니다.|
|[타이머](/dotnet/api/system.windows.forms.timer)|[DispatcherTimer](/dotnet/api/system.windows.threading.dispatchertimer)|Device. StartTime ()|
|[ToolStrip](/dotnet/api/system.windows.forms.toolstrip)|[]](/dotnet/api/system.windows.controls.toolbar)|페이지. 페이지 및 기타 항목|
|[ToolStripContainer](/dotnet/api/system.windows.forms.toolstripcontainer), [ToolStripDropDown](/dotnet/api/system.windows.forms.toolstripdropdown), [ToolStripDropDownMenu](/dotnet/api/system.windows.forms.toolstripdropdownmenu), [ToolStripPanel](/dotnet/api/system.windows.forms.toolstrippanel)|컴퍼지션이 포함 된 [도구 모음](/dotnet/api/system.windows.controls.toolbar) 입니다.|컴퍼지션을 포함 하는 페이지 및 기타 항목 페이지|
|[ToolTip](/dotnet/api/system.windows.forms.tooltip)|[ToolTip](/dotnet/api/system.windows.controls.tooltip)|내게 필요한 옵션 기능 사용|
|[TrackBar](/dotnet/api/system.windows.forms.trackbar)|[슬라이더](/dotnet/api/system.windows.controls.slider)|슬라이더|
|[TreeView](/dotnet/api/system.windows.forms.treeview)|[TreeView](/dotnet/api/system.windows.controls.treeview)|NavigationPage에서 계층적 ListView 고려|
|[UserControl](/dotnet/api/system.windows.forms.usercontrol)|[UserControl](/dotnet/api/system.windows.controls.usercontrol)|보기 및 사용자 지정 렌더러|
|[VScrollBar](/dotnet/api/system.windows.forms.vscrollbar)|[스크롤 막대](/dotnet/api/system.windows.controls.primitives.scrollbar)|ScrollView 사용|
|[WebBrowser](/dotnet/api/system.windows.forms.webbrowser)|[WebBrowser](/dotnet/api/system.windows.controls.webbrowser)|WebView|