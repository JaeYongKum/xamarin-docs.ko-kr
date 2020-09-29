---
title: Xamarin.ios에서 자연어 프레임 워크 사용
description: 이 문서에서는 자연어 프레임 워크에 대해 설명 합니다. IOS 12에 도입 된 자연어 프레임 워크는 언어 인식, 음성 식별 부분 및 명명 된 엔터티 인식에 사용할 수 있는 기본 iOS API입니다.
ms.prod: xamarin
ms.assetid: 126C8764-F873-4EB9-98A3-D82AB5689111
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 08/20/2018
ms.openlocfilehash: 3d559f197ffc1696c4fd9f7beff7b107103142d3
ms.sourcegitcommit: 00e6a61eb82ad5b0dd323d48d483a74bedd814f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91434196"
---
# <a name="using-the-natural-language-framework-with-xamarinios"></a>Xamarin.ios에서 자연어 프레임 워크 사용

IOS 12에서 도입 된 자연어 프레임 워크는 장치 자연어 처리를 가능 하 게 합니다. 언어 인식, 토큰화 및 태그 지정을 지원 합니다. 토큰화는 텍스트를 해당 구성 요소 단어, 문장 또는 단락으로 분할 합니다. 태그 지정은 음성, 사람, 장소 및 조직의 일부를 식별 합니다.

또한 자연어 프레임 워크는 사용자 지정 핵심 ML 모델을 사용 하 여 특수 컨텍스트에서 텍스트를 분류 하 고 태그를 지정할 수 있습니다.

[NSLinguisticTagger](xref:Foundation.NSLinguisticTagger) 클래스는 계속 사용할 수 있습니다. 그러나 자연어를 처리 하는 데 사용 하는 기본 메커니즘은 자연어 프레임 워크입니다.

## <a name="sample-app-xamarinnl"></a>샘플 앱: XamarinNL

Xamarin.ios에서 자연어 프레임 워크를 사용 하는 방법을 알아보려면 [XamarinNL 샘플 앱](/samples/xamarin/ios-samples/ios12-xamarinnl)을 살펴보세요.
이 샘플 앱에서는 자연어 프레임 워크를 사용 하 여 다음을 수행 하는 방법을 보여 줍니다.

- [인식 언어](#recognizing-languages).
- [텍스트를 단어와 문장으로 토큰화](#tokenizing-text-into-words-sentences-and-paragraphs).
- [명명 된 엔터티 및 음성 부분에 태그를 지정](#tagging-named-entities-and-parts-of-speech)합니다.

## <a name="recognizing-languages"></a>언어 인식

샘플 앱의 **인식기** 탭에서는 [`NLLanguageRecognizer`](xref:NaturalLanguage.NLLanguageRecognizer)
텍스트 블록의 언어를 결정 하는입니다.

> [!NOTE]
> 언어 인식은 특정 유형의 텍스트 분류입니다. 자연어 프레임 워크는 개발자가 제공 하는 핵심 ML 모델을 통해 사용자 지정 텍스트 분류도 지원 합니다. 자세한 내용은 WWDC 2018에서 [자연어 프레임 워크 세션 소개](https://developer.apple.com/videos/play/wwdc2018/713/) 를 참조 하세요.

### <a name="dominant-language"></a>주요 언어

**언어** 단추를 탭 하 여 사용자 입력의 기준 언어를 식별 합니다.

`HandleDetermineLanguageButtonTap`의 메서드 `LanguageRecognizerViewController` 는[`GetDominantLanguage`](xref:NaturalLanguage.NLLanguageRecognizer.GetDominantLanguage*)
를 가져올의 메서드 `NLLanguageRecognizer`[`NLLanguage`](xref:NaturalLanguage.NLLanguage)
텍스트에 있는 주 언어의 경우:

```csharp
partial void HandleDetermineLanguageButtonTap(UIButton sender)
{
    UserInput.ResignFirstResponder();
    if (!String.IsNullOrWhiteSpace(UserInput.Text))
    {
        NLLanguage lang = NLLanguageRecognizer.GetDominantLanguage(UserInput.Text);
        DominantLanguageLabel.Text = lang.ToString();
    }
}
```

### <a name="language-probabilities"></a>언어 확률

**언어 확률** 단추를 탭 하 여 사용자 입력에 대 한 언어 가설 목록을 페치합니다.

`HandleLanguageProbabilitiesButtonTap`클래스의 메서드는를 `LanguageRecognizerViewController` 인스턴스화하고 `NLLanguageRecognizer` 에 요청 합니다.[`Process`](xref:NaturalLanguage.NLLanguageRecognizer.Process*)
사용자의 텍스트입니다. 그런 다음 언어 인식기를 호출 합니다. [`GetNativeLanguageHypotheses`](xref:NaturalLanguage.NLLanguageRecognizer.GetNativeLanguageHypotheses*)
메서드-언어 사전 및 관련 확률을 페치합니다. `LanguageRecognizerTableViewController`그런 다음 클래스는 이러한 언어 및 확률을 렌더링 합니다.

```csharp
partial void HandleLanguageProbabilitiesButtonTap(UIButton sender)
{
    UserInput.ResignFirstResponder();
    if (!String.IsNullOrWhiteSpace(UserInput.Text))
    {
        var recognizer = new NLLanguageRecognizer();
        recognizer.Process(UserInput.Text);
        NSDictionary<NSString, NSNumber> probabilities = recognizer.GetNativeLanguageHypotheses(10);
        PerformSegue(ShowLanguageProbabilitiesSegue, this);
    }
}
```

가능한 `NLLanguage` 값은 다음과 같습니다.

- `Amharic`
- `Arabic`
- `Armenian`
- `Bengali`
- `Bulgarian`
- `Burmese`
- `Catalan`
- `Cherokee`
- `Croatian`
- `Czech`
- `Danish`
- `Dutch`
- `English`
- `Finnish`
- `French`
- `Georgian`
- `German`
- `Greek`
- `Gujarati`
- `Hebrew`
- `Hindi`
- `Hungarian`
- `Icelandic`
- `Indonesian`
- `Italian`
- `Japanese`
- `Kannada`
- `Khmer`
- `Korean`
- `Lao`
- `Malay`
- `Malayalam`
- `Marathi`
- `Mongolian`
- `Norwegian`
- `Oriya`
- `Persian`
- `Polish`
- `Portuguese`
- `Punjabi`
- `Romanian`
- `Russian`
- `SimplifiedChinese`
- `Sinhalese`
- `Slovak`
- `Spanish`
- `Swedish`
- `Tamil`
- `Telugu`
- `Thai`
- `Tibetan`
- `TraditionalChinese`
- `Turkish`
- `Ukrainian`
- `Undetermined`
- `Urdu`
- `Vietnamese`

지원 되는 언어의 전체 목록은 다음의 일부로 제공 됩니다. [`NLLanguage`](xref:NaturalLanguage.NLLanguage)
API 설명서를 열거 합니다.

## <a name="tokenizing-text-into-words-sentences-and-paragraphs"></a>단어, 문장 및 단락에 텍스트 토큰화

샘플 앱의 **토크 토크** 탭에서는 텍스트 블록을를 사용 하 여 해당 구성 요소 단어나 문장으로 구분 하는 방법을 보여 줍니다 [`NLTokenizer`](xref:NaturalLanguage.NLTokenizer) .

**단어** 또는 **문장** 단추를 탭 하 여 토큰 목록을 페치합니다. 각 토큰은 원래 텍스트의 단어나 문장과 연결 됩니다.

`ShowTokens` 을 호출 하 여 사용자의 입력을 토큰으로 분할 합니다. [`GetTokens`](xref:NaturalLanguage.NLTokenizer.GetTokens*)
의 메서드입니다 `NLTokenizer` . 이 메서드는 다음의 배열을 반환 합니다. [`NSValue`](xref:Foundation.NSValue)
각각 `NSRange` 원래 텍스트의 토큰에 해당 하는 값을 래핑하는 개체입니다.

```csharp
void ShowTokens(NLTokenUnit unit)
{
    if (!String.IsNullOrWhiteSpace(UserInput.Text))
    {
        var tokenizer = new NLTokenizer(unit);
        tokenizer.String = UserInput.Text;
        var range = new NSRange(0, UserInput.Text.Length);
        NSValue[] tokens = tokenizer.GetTokens(range);
        PerformSegue(ShowTokensSegue, this);
    }
}
```

`LanguageTokenizerTableViewController` 각 테이블 셀에서 단일 토큰을 렌더링 합니다. `NSRange`토큰에서를 추출 하 고 `NSValue` , 원래 텍스트에서 해당 문자열을 찾은 다음 테이블 뷰 셀에 레이블을 설정 합니다.

```csharp
public override UITableViewCell GetCell(UITableView tableView, NSIndexPath indexPath)
{
    var cell = TableView.DequeueReusableCell(TokenCell);
    NSRange range = Tokens[indexPath.Row].RangeValue;
    cell.TextLabel.Text = Text.Substring((int)range.Location, (int)range.Length);
    return cell;
}
```

## <a name="tagging-named-entities-and-parts-of-speech"></a>명명 된 엔터티 및 음성 부분 태그 지정

XamarinNL 샘플 앱의 **태거** 탭은 [`NLTagger`](xref:NaturalLanguage.NLTagger)
범주를 입력 문자열의 토큰과 연결 하는 클래스입니다.
자연어 프레임 워크에는 사람, 장소, 조직 및 음성 부분을 인식 하기 위한 기본 제공 지원이 포함 됩니다.

> [!NOTE]
> 또한 자연어 프레임 워크는 개발자가 제공 하는 핵심 ML 모델을 통해 사용자 지정 태깅 스키마를 지원 합니다. 자세한 내용은 WWDC 2018에서 [자연어 프레임 워크 세션 소개](https://developer.apple.com/videos/play/wwdc2018/713/) 를 참조 하세요.

인출 하려면 **명명 된 엔터티** 또는 **음성 부분** 단추를 누릅니다.

- `NSValue` `NSRange` 원본 텍스트의 토큰에 대해를 래핑하는 개체의 배열입니다.
- [`NLTag`](xref:NaturalLanguage.NLTag)동일한 배열 인덱스에서 토큰에 대 한 범주-값의 배열 `NSValue` 입니다.

`LanguageTaggerViewController`및의 `HandlePartsOfSpeechButtonTap` `HandleNamedEntitiesButtonTap` 각 호출은 `ShowTags` [`NLTagScheme`](xref:NaturalLanguage.NLTagScheme) `NLTagScheme.LexicalClass` (음성 부분) 또는 `NLTagScheme.NameType` (명명 된 엔터티의 경우)을 통해 전달 됩니다.

`ShowTags` 을 만들어 `NLTagger` `NLTagScheme` 쿼리할 형식의 배열 (이 경우에는 전달 된 값만)을 사용 하 여 인스턴스화합니다 `NLTagScheme` . 그런 다음 [`GetTags`](xref:NaturalLanguage.NLTagger.GetTags*)
에서 메서드를 사용 `NLTagger` 하 여 사용자 입력의 텍스트와 관련 된 태그를 확인 합니다.

```csharp
void ShowTags(NLTagScheme tagScheme)
{
    if (!String.IsNullOrWhiteSpace(UserInput.Text))
    {
        var tagger = new NLTagger(new NLTagScheme[] { tagScheme });
        var range = new NSRange(0, UserInput.Text.Length);
        tagger.String = UserInput.Text;

        NLTag[] tags = tagger.GetTags(range, NLTokenUnit.Word, tagScheme, NLTaggerOptions.OmitWhitespace, out NSValue[] ranges);
        NSValue[] tokenRanges = ranges;
        detailViewTitle = tagScheme == NLTagScheme.NameType ? "Named Entities" : "Parts of Speech";

        PerformSegue(ShowEntitiesSegue, this);
    }
}
```

그러면 태그가에 의해 테이블에 표시 됩니다 `LanguageTaggerTableViewController` .

가능한 `NLTag` 값은 다음과 같습니다.

- `Adjective`
- `Adverb`
- `Classifier`
- `CloseParenthesis`
- `CloseQuote`
- `Conjunction`
- `Dash`
- `Determiner`
- `Idiom`
- `Interjection`
- `Noun`
- `Number`
- `OpenParenthesis`
- `OpenQuote`
- `OrganizationName`
- `Other`
- `OtherPunctuation`
- `OtherWhitespace`
- `OtherWord`
- `ParagraphBreak`
- `Particle`
- `PersonalName`
- `PlaceName`
- `Preposition`
- `Pronoun`
- `Punctuation`
- `SentenceTerminator`
- `Verb`
- `Whitespace`
- `Word`
- `WordJoiner`

지원 되는 태그의 전체 목록은 다음의 일부로 제공 됩니다. [`NLTag`](xref:NaturalLanguage.NLTag)
API 설명서를 열거 합니다.

## <a name="related-links"></a>관련 링크

- [샘플 앱-XamarinNL](/samples/xamarin/ios-samples/ios12-xamarinnl)
- [자연어 프레임 워크 소개](https://developer.apple.com/videos/play/wwdc2018/713/)
- [자연어 (Apple)](https://developer.apple.com/documentation/naturallanguage?language=objc)