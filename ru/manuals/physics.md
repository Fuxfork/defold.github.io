---
layout: manual
language: ru
github: https://github.com/defold/doc
title: Физика
brief: В состав Defold входят 2D и 3D физические движки. Они позволяют симулировать ньютоновские физические взаимодействия между разными типами объектов столкновения.
---

# Физика

Defold включает модифицированную версию физического движка [Box2D](http://www.box2d.org) (версия 2.1) для симуляций 2D-физики, а также физический движок Bullet (версии 2.77) для 3D-физики. Это позволяет симулировать ньютоновские физические взаимодействия между разными типами _объектов столкновения_. Данное руководство объясняет принцип работы этих движков.

Основные концепции физических движков, задействованных в Defold следующие:

* **Объекты столкновения** --- Объект столкновения является компонентом, который применяется для придания игровому объекту физического поведения. Объект столкновения обладает физическими свойствами, такими, как вес, трение и форма. [Узнайте, как создаются объекты столкновений](/ru/manuals/physics-objects).
* **Формы столкновения** --- Объект столкновения может использовать либо несколько геометрических примитивов-форм либо одну сложную форму, определяющую пространственные пределы объекта. [Узнайте, как добавлять формы к объектам столкновений](/ru/manuals/physics-shapes).
* **Группы столкновений** --- Все объекты столкновения должны принадлежать предопределенной группе и каждый объект столкновения может определять список других групп, с которыми он может сталкиваться. [Узнайте, как использовать группы столкновений](/ru/manuals/physics-groups).
* **Сообщения столкновения** --- Когда два объекта столкновений сталкиваются, физический движок посылает сообщения игровым объектам, которым принадлежат эти два компонента. [Узнайте больше о сообщениях о столкновения](/ru/manuals/physics-messages).

В дополнении к объектам столкновения также можно задать **ограничения** объектов столкновения, более известные как **сочленения** (joints), чтобы соединить два объекта столкновения и ограничить или иными способами направить силу и повлиять на то, как они ведут себя в физической симуляции. [Узнайте больше о сочленениях](/ru/manuals/physics-joints).

Вы также можете прощупывать и считывать физический мир вдоль линейного луча известного как **проекционный луч**. [Узнайте больше о проекционных лучах](/ru/manuals/physics-ray-casts).


## Единицы измерения, применяемые физическими движками

Физические движки симулируют ньютоновскую физику и спроектированы для гладкой работы с метрами, килограммами и секундами (мкс) в качестве единиц измерения. Более того, физический движок откалиброван, чтобы гладко работать с движущимися объектами размеров в диапазоне от 0.1 до 10 метров (статические объекты могут быть больше), и по умолчанию движок трактует 1 единицу (пиксель) как 1 метр. Конвертация между пикселями и метрами удобна на уровне симуляции, но с точки зрения создания игры --- это не очень полезно. Со стандартными настройками форма столкновений размером в 200 пикселей будет трактоваться как имеющая размер 200 метров, что далеко за пределами рекомендуемого диапазона, по крайней мере для движущегося объекта.

В целом, требуется, чтобы физическая симуляция была отмасштабирована для того, чтобы гладко работать с типовым размером объектов в игре. Масштаб физической симуляции может быть изменен в файле `game.project` в [настройках масштаба физики](/ru/manuals/project-settings/#physics). Выставление этого значения в, например 0.02, будет означать, что 200 пикселей будут трактоваться как 4 метра. Учтите также, что гравитация (также меняется в `game.project`) должна быть увеличена для согласования с измененным масштабом.


## Предостережения и типовые проблемы

Прокси-коллекции
: Через прокси-коллекции возможно загрузить более одной коллекции верхнего уровня или *игрового мира* в движок. Поступая так, важно держать в уме то, что каждая коллекция верхнего уровня --- это отдельный физический мир. Физические взаимодействия ([коллизии, триггеры](/ru/manuals/physics-messages) и [проекционные лучи](/ru/manuals/physics-ray-casts)) срабатывают только для объектов принадлежащих одному и тому же миру. Поэтому, даже если объекты столкновений из двух разных миров визуально располагаются один над другим, никакие физические взаимодействия между ними просчитываться не будут.

Столкновения не определяются
: Если вы испытываете проблемы с тем, что столкновения не обрабатываются или не детектируются, то убедитесь, что вам знаком весь материал из секции по [отладке физики в руководстве по отладке](/ru/manuals/debugging/#debugging-problems-with-physics).