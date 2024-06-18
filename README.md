# «Классификация баллистических объектов по радиолокационным данным»  
Нейронные сети хороши в задачах, где затраты на формализацию алгоритма велики, но присутствует большое количество входных и соответствующих им выходных воздействий, так как для работы нейронной сети необходим только набор входных и выходных данных.\
Одной из сфер деятельности, где существуют трудно формализуемые задачи, является радиолокация. Использование нейронных сетей для решения задач радиолокации может повысить эффективность классификации объектов.\
На данный момент задачу классификации может решить оператор радиолокационной станции, либо заранее написанный алгоритм. Оба варианта имеют свои недостатки: эффективность оператора при большом количестве баллистических объектов резко падает и становится недостаточной, при использовании алгоритмов такой проблемы нет, но возникает проблема формализации алгоритма, при появлении новых типов объектов, так как при их появлении необходимо в виде алгоритма или формулы определить процесс классификации данного объекта, что зачастую является нетривиальной задачей.
## Задание
Целью работы является обработка предоставленного набора данных, разработка архитектуры нейронной сети, выбор оптимальных гиперпараметров модели, обучение нейронной сети и проверка результатов обучения.
## План выполнения 
1.	Анализ и обработка набора входных и выходных данных\
Набор данных для обучения модели представляет собой CSV-файл, содержащий порядка 1.8 миллиона записей.
<table id="tabular">
<tbody>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: center; border-left-style: solid !important; border-left-width: 1px !important; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top-style: solid !important; border-top-width: 1px !important; width: auto; vertical-align: middle; " class="_empty"></td>
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top-style: solid !important; border-top-width: 1px !important; width: auto; vertical-align: middle; ">Обозначение</td>
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top-style: solid !important; border-top-width: 1px !important; width: auto; vertical-align: middle; ">Описание</td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: center; border-left-style: solid !important; border-left-width: 1px !important; border-right-style: solid !important; border-right-width: 1px !important; border-bottom: none !important; border-top: none !important; width: auto; border-bottom-style: solid !important; border-bottom-width: 1px !important; " rowspan="8"><div class="inline-tabular sub-table"><table id="tabular">
<tbody>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: left; border-left: none !important; border-bottom: none !important; border-top: none !important; width: auto; vertical-align: middle; ">Входные</td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: left; border-left: none !important; border-bottom: none !important; border-top: none !important; width: auto; vertical-align: middle; ">данные</td>
</tr>
</tbody>
</table>
<tsv style="display: none">Входные
данные</tsv><table-markdown style="display: none">| Входные |
| :--- |
| данные |</table-markdown><csv style="display: none">Входные
данные</csv></div></td>
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; "><span class="math-inline "><mathml style="display: none"><math xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi mathvariant="normal">X</mi>
  </mrow>
</math></mathml><mathmlword style="display: none"><math xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi mathvariant="normal">X</mi>
  </mrow>
</math></mathmlword><asciimath style="display: none;">X</asciimath><mjx-container class="MathJax" jax="SVG"><svg xmlns="http://www.w3.org/2000/svg" width="1.697ex" height="1.545ex" role="img" focusable="false" viewBox="0 -683 750 683" style="vertical-align: 0px;"><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><g data-mml-node="math"><g data-mml-node="TeXAtom" data-mjx-texclass="ORD"><g data-mml-node="mi"><path data-c="58" d="M270 0Q252 3 141 3Q46 3 31 0H23V46H40Q129 50 161 88Q165 94 244 216T324 339Q324 341 235 480T143 622Q133 631 119 634T57 637H37V683H46Q64 680 172 680Q297 680 318 683H329V637H324Q307 637 286 632T263 621Q263 618 322 525T384 431Q385 431 437 511T489 593Q490 595 490 599Q490 611 477 622T436 637H428V683H437Q455 680 566 680Q661 680 676 683H684V637H667Q585 634 551 599Q548 596 478 491Q412 388 412 387Q412 385 514 225T620 62Q628 53 642 50T695 46H726V0H717Q699 3 591 3Q466 3 445 0H434V46H440Q454 46 476 51T499 64Q499 67 463 124T390 238L353 295L350 292Q348 290 343 283T331 265T312 236T286 195Q219 88 218 84Q218 70 234 59T272 46H280V0H270Z"></path></g></g></g></g></svg></mjx-container></span></td>
<td style="text-align: center; border-left-style: solid !important; border-left-width: 1px !important; border-right-style: solid !important; border-right-width: 1px !important; border-bottom: none !important; border-top: none !important; width: auto; border-bottom-style: solid !important; border-bottom-width: 1px !important; " rowspan="3"><div class="inline-tabular sub-table"><table id="tabular">
<tbody>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: left; border-left: none !important; border-bottom: none !important; border-top: none !important; width: auto; vertical-align: middle; ">Координаты баллистического объекта в</td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: left; border-left: none !important; border-bottom: none !important; border-top: none !important; width: auto; vertical-align: middle; ">местной прямоугольной системе координат</td>
</tr>
</tbody>
</table>
<tsv style="display: none">Координаты баллистического объекта в
местной прямоугольной системе координат</tsv><table-markdown style="display: none">| Координаты баллистического объекта в |
| :--- |
| местной прямоугольной системе координат |</table-markdown><csv style="display: none">Координаты баллистического объекта в
местной прямоугольной системе координат</csv></div></td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; "><span class="math-inline "><mathml style="display: none"><math xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi mathvariant="normal">Y</mi>
  </mrow>
</math></mathml><mathmlword style="display: none"><math xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi mathvariant="normal">Y</mi>
  </mrow>
</math></mathmlword><asciimath style="display: none;">Y</asciimath><mjx-container class="MathJax" jax="SVG"><svg xmlns="http://www.w3.org/2000/svg" width="1.697ex" height="1.545ex" role="img" focusable="false" viewBox="0 -683 750 683" style="vertical-align: 0px;"><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><g data-mml-node="math"><g data-mml-node="TeXAtom" data-mjx-texclass="ORD"><g data-mml-node="mi"><path data-c="59" d="M518 0Q497 3 374 3Q253 3 232 0H221V46H254Q313 47 321 58Q324 62 324 167V273L221 446Q117 620 114 623Q106 631 91 634T31 637H11V683H20Q29 680 148 680Q273 680 294 683H305V637H287Q239 636 236 621Q236 619 321 475L407 332L483 460Q502 492 527 534Q563 594 563 604Q563 632 517 637H508V683H517H525Q533 683 545 683T571 682T600 681T626 681Q695 681 731 683H738V637H723Q640 633 613 588Q612 587 517 427L425 273V169V95Q425 66 428 59T444 49Q459 46 506 46H528V0H518Z"></path></g></g></g></g></svg></mjx-container></span></td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; "><span class="math-inline "><mathml style="display: none"><math xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi mathvariant="normal">Z</mi>
  </mrow>
</math></mathml><mathmlword style="display: none"><math xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi mathvariant="normal">Z</mi>
  </mrow>
</math></mathmlword><asciimath style="display: none;">Z</asciimath><mjx-container class="MathJax" jax="SVG"><svg xmlns="http://www.w3.org/2000/svg" width="1.382ex" height="1.545ex" role="img" focusable="false" viewBox="0 -683 611 683" style="vertical-align: 0px;"><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><g data-mml-node="math"><g data-mml-node="TeXAtom" data-mjx-texclass="ORD"><g data-mml-node="mi"><path data-c="5A" d="M69 443Q69 452 74 554T80 683H549Q555 677 555 664Q555 649 554 648Q552 645 366 348T179 50T192 49T263 49H275H302Q333 49 353 50T401 59T447 78T482 115T507 173Q513 200 520 273V282H560V274Q560 272 552 143T543 8V0H302L61 1L58 3Q55 8 55 21V35Q59 43 153 193T340 489T432 637H343Q259 637 214 625T141 573Q109 523 109 445Q109 443 89 443H69Z"></path></g></g></g></g></svg></mjx-container></span></td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; ">VX</td>
<td style="text-align: center; border-left-style: solid !important; border-left-width: 1px !important; border-right-style: solid !important; border-right-width: 1px !important; border-bottom: none !important; border-top: none !important; width: auto; border-bottom-style: solid !important; border-bottom-width: 1px !important; " rowspan="3"><div class="inline-tabular sub-table"><table id="tabular">
<tbody>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: left; border-left: none !important; border-bottom: none !important; border-top: none !important; width: auto; vertical-align: middle; ">Составляющие вектора скорости</td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: left; border-left: none !important; border-bottom: none !important; border-top: none !important; width: auto; vertical-align: middle; ">баллистического объекта в местной</td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: left; border-left: none !important; border-bottom: none !important; border-top: none !important; width: auto; vertical-align: middle; ">прямоугольной системе координат</td>
</tr>
</tbody>
</table>
<tsv style="display: none">Составляющие вектора скорости
баллистического объекта в местной
прямоугольной системе координат</tsv><table-markdown style="display: none">| Составляющие вектора скорости |
| :--- |
| баллистического объекта в местной |
| прямоугольной системе координат |</table-markdown><csv style="display: none">Составляющие вектора скорости
баллистического объекта в местной
прямоугольной системе координат</csv></div></td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; ">VY</td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; "><span class="math-inline "><mathml style="display: none"><math xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi mathvariant="normal">V</mi>
    <mi mathvariant="normal">Z</mi>
  </mrow>
</math></mathml><mathmlword style="display: none"><math xmlns="http://www.w3.org/1998/Math/MathML">
  <mrow>
    <mi mathvariant="normal">V</mi>
    <mi mathvariant="normal">Z</mi>
  </mrow>
</math></mathmlword><asciimath style="display: none;">VZ</asciimath><mjx-container class="MathJax" jax="SVG"><svg xmlns="http://www.w3.org/2000/svg" width="3.079ex" height="1.595ex" role="img" focusable="false" viewBox="0 -683 1361 705" style="vertical-align: -0.05ex;"><g stroke="currentColor" fill="currentColor" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><g data-mml-node="math"><g data-mml-node="TeXAtom" data-mjx-texclass="ORD"><g data-mml-node="mi"><path data-c="56" d="M114 620Q113 621 110 624T107 627T103 630T98 632T91 634T80 635T67 636T48 637H19V683H28Q46 680 152 680Q273 680 294 683H305V637H284Q223 634 223 620Q223 618 313 372T404 126L490 358Q575 588 575 597Q575 616 554 626T508 637H503V683H512Q527 680 627 680Q718 680 724 683H730V637H723Q648 637 627 596Q627 595 515 291T401 -14Q396 -22 382 -22H374H367Q353 -22 348 -14Q346 -12 231 303Q114 617 114 620Z"></path></g><g data-mml-node="mi" transform="translate(750, 0)"><path data-c="5A" d="M69 443Q69 452 74 554T80 683H549Q555 677 555 664Q555 649 554 648Q552 645 366 348T179 50T192 49T263 49H275H302Q333 49 353 50T401 59T447 78T482 115T507 173Q513 200 520 273V282H560V274Q560 272 552 143T543 8V0H302L61 1L58 3Q55 8 55 21V35Q59 43 153 193T340 489T432 637H343Q259 637 214 625T141 573Q109 523 109 445Q109 443 89 443H69Z"></path></g></g></g></g></svg></mjx-container></span></td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; ">epr</td>
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; "><div class="inline-tabular sub-table"><table id="tabular">
<tbody>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: left; border-left: none !important; border-bottom: none !important; border-top: none !important; width: auto; vertical-align: middle; ">Эффективная площадь рассеяния (ЭПР)</td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: left; border-left: none !important; border-bottom: none !important; border-top: none !important; width: auto; vertical-align: middle; ">объекта</td>
</tr>
</tbody>
</table>
<tsv style="display: none">Эффективная площадь рассеяния (ЭПР)
объекта</tsv><table-markdown style="display: none">| Эффективная площадь рассеяния (ЭПР) |
| :--- |
| объекта |</table-markdown><csv style="display: none">Эффективная площадь рассеяния (ЭПР)
объекта</csv></div></td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; ">gamma</td>
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; ">Баллистический коэффициент объекта</td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: center; border-left-style: solid !important; border-left-width: 1px !important; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; "><div class="inline-tabular sub-table"><table id="tabular">
<tbody>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: left; border-left: none !important; border-bottom: none !important; border-top: none !important; width: auto; vertical-align: middle; ">Выходные</td>
</tr>
<tr style="border-top: none !important; border-bottom: none !important;">
<td style="text-align: left; border-left: none !important; border-bottom: none !important; border-top: none !important; width: auto; vertical-align: middle; ">данные</td>
</tr>
</tbody>
</table>
<tsv style="display: none">Выходные
данные</tsv><table-markdown style="display: none">| Выходные |
| :--- |
| данные |</table-markdown><csv style="display: none">Выходные
данные</csv></div></td>
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; ">type</td>
<td style="text-align: center; border-right-style: solid !important; border-right-width: 1px !important; border-bottom-style: solid !important; border-bottom-width: 1px !important; border-top: none !important; width: auto; vertical-align: middle; ">Тип баллистического объекта</td>
</tr>
</tbody>
</table>
Этот набор данных следует преобразовать для повышения качества и эффективности обучения
2.	Разработка архитектуры модели нейронной сети.
Используем модель c полносвязными слоями, функцией активации relu в промежуточных слоях и функцией softmax в выходном слое. В качестве оптимизатора возьмем rmsprop, функция потерь categorical_crossentropy. 
3.	Подбор количества промежуточных слоёв в модели, количества нейронов в каждом слое, размера пакета и прочих гиперпараметров для улучшения характеристик обучения модели – величина функции потерь (loss) и точность (accuracy).
4.  Оценим и визуализируем результаты обучения (кривая обучения по функции потерь и точности)
5.  Разработаем автокодировщик для предоставленного набора данных и визуализируем его внутреннее представление (количество нейронов во внутреннем слое возьмем 2).
|  | Обозначение | Описание |
| :---: | :---: | :---: |
| Входные <br> данные | $\mathrm{X}$ | Координаты баллистического объекта в <br> местной прямоугольной системе координат |
|  | $\mathrm{Y}$ |  |
|  | $\mathrm{Z}$ |  |
|  | VX | Составляющие вектора скорости <br> баллистического объекта в местной <br> прямоугольной системе координат |
|  | VY |  |
|  | $\mathrm{VZ}$ |  |
|  | epr | Эффективная площадь рассеяния (ЭПР) <br> объекта |
|  | gamma | Баллистический коэффициент объекта |
| Выходные <br> данные | type | Тип баллистического объекта |
