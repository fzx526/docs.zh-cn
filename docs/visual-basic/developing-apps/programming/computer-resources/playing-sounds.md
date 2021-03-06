---
title: 播放声音 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- system sounds, playing
- system sounds
- playing sounds, Visual Basic
- sound loops
- My.Computer.Audio object, tasks
- sounds, playing
- sounds, background
- playing sounds
ms.assetid: f0d9e4ab-57c7-47b6-86d3-99ff07078040
ms.openlocfilehash: decd845fde5bd4fad702cfe05fd63fcc180b63a6
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="playing-sounds-visual-basic"></a>播放声音 (Visual Basic)
`My.Computer.Audio` 对象提供用于播放声音的方法。  
  
## <a name="playing-sounds"></a>播放声音  
 应用程序可通过背景播放在播放声音时执行其他代码。 `My.Computer.Audio.Play` 方法允许应用程序一次仅播放一种背景声音；应用程序播放新背景声音时，会停止播放上一种背景声音。 你也可以播放一种声音并等待其播放完毕。  
  
 下例中使用 `My.Computer.Audio.Play` 方法播放声音。 指定 `AudioPlayMode.WaitToComplete` 时，`My.Computer.Audio.Play` 将等待声音播放完毕，然后再调用代码继续。 使用此示例时，应确保文件名可指代计算机中的 .wav 声音文件  
  
 [!code-vb[VbVbalrMyComputer#15](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_1.vb)]  
  
 下例中使用 `My.Computer.Audio.Play` 方法播放声音。 使用此示例时，应确保应用程序资源包含名为 Waterfall 的 .wav 声音文件。  
  
 [!code-vb[VbVbalrMyComputer#16](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_2.vb)]  
  
## <a name="playing-looping-sounds"></a>播放循环声音  
 在下例中，指定 `PlayMode.BackgroundLoop` 时，`My.Computer.Audio.Play` 方法将播放指定的背景声音。 使用此示例时，应确保文件名可指代计算机中的 .wav 声音文件。  
  
 [!code-vb[VbVbalrMyComputer#11](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_3.vb)]  
  
 在下例中，指定 `PlayMode.BackgroundLoop` 时，`My.Computer.Audio.Play` 方法将播放指定的背景声音。 使用此示例时，应确保应用程序资源包含名为 Waterfall 的 .wav 声音文件。  
  
 [!code-vb[VbVbalrMyComputer#12](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_4.vb)]  
  
 前面的代码示例也可作为 IntelliSense 代码片段。 在代码片段选取器中，它位于“Windows 窗体应用程序”>“声音”中。 有关详细信息，请参阅[代码片段](/visualstudio/ide/code-snippets)。  
  
 一般情况下，应用程序播放循环声音时，声音最终将停止。  
  
## <a name="stopping-the-playing-of-sounds-in-the-background"></a>停止播放背景声音  
 使用 `My.Computer.Audio.Stop` 方法可停止应用程序当前播放的背景声音或循环声音。  
  
 一般情况下，应用程序播放循环声音时，声音将在某个时间点停止。  
  
 下面的示例将停止播放背景声音。  
  
 [!code-vb[VbVbalrMyComputer#18](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_5.vb)]  
  
 前面的代码示例也可作为 IntelliSense 代码片段。 在代码片段选取器中，它位于“Windows 窗体应用程序”>“声音”中。 有关详细信息，请参阅[代码片段](/visualstudio/ide/code-snippets)。  
  
## <a name="playing-system-sounds"></a>播放系统声音  
 使用 `My.Computer.Audio.PlaySystemSound` 方法可播放指定的系统声音。  
  
 `My.Computer.Audio.PlaySystemSound` 方法将作为 <xref:System.Media.SystemSound> 类中的共享成员之一的参数。 系统声音 <xref:System.Media.SystemSounds.Asterisk%2A> 通常表示错误。  
  
 下例使用 `My.Computer.Audio.PlaySystemSound` 方法播放系统声音。  
  
 [!code-vb[VbVbalrMyComputer#17](../../../../visual-basic/developing-apps/programming/computer-resources/codesnippet/VisualBasic/playing-sounds_6.vb)]  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualBasic.Devices.Audio>  
 <xref:Microsoft.VisualBasic.Devices.Audio.Play%2A>  
 <xref:Microsoft.VisualBasic.Devices.Audio.PlaySystemSound%2A>  
 <xref:Microsoft.VisualBasic.Devices.Audio.Stop%2A>  
 <xref:Microsoft.VisualBasic.AudioPlayMode>
