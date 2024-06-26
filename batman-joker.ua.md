# Значення, що повертається, проти побічного ефекту.
### Приклад з Бетменом та Джокером

## [Русский](batman-joker.ru.md) | [English](README.md) | Українська

Є два основних способи написання функцій на JavaScript (і в інших мовах програмування теж, але мої приклади на JavaScript). Один спосіб - **повертати значення**, а інший - **мати побічний ефект**. І ці поняття часто плутаються або помилково розуміються початківцями. Тому давайте прояснимо це на прикладі. І оскільки такі типи функцій часто називають **чистими функціями** та **брудними функціями**, я (некомерційно) використаю аналогію з Бетменом та Джокером, оскільки вони, можливо, найбільш відомі чистий та підступний персонажі в світі. І у Джокера дійсно багато брудних трюків в рукаві, чи не так?

Бетмен завжди прикладає максимум зусиль, щоб не тільки боротися зі злочинністю, але й привести злочинців до справедливості, живими. І результат завжди такий, якого слід очікувати: вони в решті решт втікають із в'язниці або психіатричної лікарні, і Бетмен завжди готовий повернути їх назад. Тим не менше, його дії завжди передбачувані, і він ніколи не робить нічого несподіваного. І всі його перемоги нічого не змінюють у світі або навіть в Готемі. Тому Бетмен завжди має привід повернутися на наші сторінки та екрани.

Джокер, з іншого боку, такий непередбачуваний. Здавалося б, навіть випадковий. Він любить робити щось несподіване, і лишає після себе безлад. Все, що Джокер робить, він робить для шоу. І він завжди залишає слід.

Тож, давайте подивимося на приклад. Ми розглянемо два набори простих функцій, які виконують одні й ті ж обчислення, але представляють результати по-різному:

```javascript

// припустімо, Бетмен, менш відомий як Брюс Вейн, мільярдер,
// вирішує обчислити середню суму коштів, які він витратив
// на свої гаджети та транспортні засоби за квартал та за рік
const january = 1000;
const february = 2000;
const march = 1200;
const april = 2600;
const may = 3000;
const june = 3100;
const july = 2700;
const august = 2500;
const september = 2300;
const october = 2900;
const november = 2200;
const december = 2100;

// Бетмен, як герой, завжди повертає результат
function bCalcQuartAvg(month1, month2, month3) {
  return (month1 + month2 + month3) / 3;
}
// завжди повертає результат!
function bCalcYearAvg(quart1, quart2, quart3, quart4) {
  return (quart1 + quart2 + quart3 + quart4) / 4;
}

// І тоді він робить свої обчислення
const q1avg = bCalcQuartAvg(january, february, march);
const q2avg = bCalcQuartAvg(april, may, june);
const q3avg = bCalcQuartAvg(july, august, september);
const q4avg = bCalcQuartAvg(october, november, december);
const yearAvg = bCalcYearAvg(q1avg, q2avg, q3avg, q4avg);

// Ми легко можемо побачити результати його обчислень
console.log({ q1avg, q2avg, q3avg, q4avg, yearAvg });
// { q1avg: 1400, q2avg: 2900, q3avg: 2500, q4avg: 2400, yearAvg: 2300 }
// і жодна з його функцій не дала побічних ефектів
```
І тепер, після того, як ми побачили, як Бетмен аналізує свої витрати на боротьбу зі злочинністю, давайте подивимося, як Джокер робить майже те саме, намагаючись підрахувати здобич зі своїх пограбувань:

```javascript
// скажімо, Джокер, як злочинний геній, вирішує
// обчислити середню суму грошей, яку він і його банда
// вкрадали протягом кварталів та року, дражнячи Бетмена
const january = 1700;
const february = 2200;
const march = 1500;
const april = 2900;
const may = 3100;
const june = 3300;
const july = 2800;
const august = 2600;
const september = 2400;
const october = 3000;
const november = 2300;
const december = 2200;

// Джокер, як хаотичний шоумен, хоче, щоб всі бачили
function jCalcQuartAvg(m1, m2, m3) {
  console.log("A-ha-ha!", (m1 + m2 + m3) / 3);
}
// але він нічого не повертає
function jCalcYearAvg(q1, q2, q3, q4) {
  console.log("BOOM!!", (q1 + q2 + q3 + q4) / 4);
}

// І тоді він робить свої обчислення...
const q1avg = jCalcQuartAvg(january, february, march);
const q2avg = jCalcQuartAvg(april, may, june);
const q3avg = jCalcQuartAvg(july, august, september);
const q4avg = jCalcQuartAvg(october, november, december);
// всі чотири константи отримали значення undefined
const yearAvg = jCalcYearAvg(q1avg, q2avg, q3avg, q4avg);

// Але ми бачимо, не те, що можна було б очікувати...
// A-ha-ha! 1800
// A-ha-ha! 3100
// A-ha-ha! 2600
// A-ha-ha! 2500
// BOOM!! NaN
```

Давайте подивимося, що тут сталося. Функції Бетмена повертали результати, дозволяючи нам використовувати їх у подальших обчисленнях. Функції Джокера, з іншого боку, просто виводили результати в консоль, і нічого не повертали. Звичайно, ми можемо побачити результати, але не можемо використовувати їх у подальших обчисленнях. Так, консоль змінилася, це побічний ефект. Але це все. Ці значення, які ми вивели туди, більше не можуть бути використані. Навіть якщо ця *брудна* функція все одно поверне значення, це не результат обчислення, а просто `undefined`. І коли ми спробували використати ці результати у подальших обчисленнях, ми отримали `NaN` (не число) як результат.

Тож якщо вам важливо лише показати результати в консолі або зберегти їх де-інде, ви можете використовувати спосіб Джокера з брудними функціями та побічними ефектами. Але якщо ви хочете використовувати результати у подальших обчисленнях, вам слід використовувати спосіб Бетмена з функціями, що повертають результати. Звичайно, технічно, ніщо не заважає вам змішувати ці два способи, але я б радив утриматися від цього. Краще, якщо ваша функція або повертає значення, або має побічний ефект, але не обидві дії одночасно. Якщо тільки ви, звичайно, не настільки досвідчені, що знаєте, що робите і чому.

Однак, Бетмен та Джокер - це лише вигадані персонажі. Не думайте, що ви не можете використовувати спосіб Джокера. Дуже часто вам доведеться змінювати користувацький інтерфейс, сортувати масиви, додавати або видаляти щось десь, відкривати або закривати модальне вікно, писати в файл, оновлювати базу даних - всі ці дії є побічними ефектами. І це абсолютно нормально. Не краще і не гірше, ніж повертати значення. Зазвичай ми так чи інакше використовуємо обидва. Просто уникайте змішування цих двох способів в одній і тій же функції, якщо можете.

**Тож якщо ви пишете функцію, почніть з того, щоб запитати себе: вам потрібно повернути значення, чи вам потрібно мати побічний ефект? І якщо ви знайомитеся з якоюсь функцією, яку не писали самі, перше, що вам слід дізнатися - чи повертає вона значення, чи має побічний ефект?**

**P.S.**: Досвідчений розробник може заперечити, що я надміру спростив поняття чистої функції, не згадавши деякі інші важливі властивості, необхідні для того, щоб назвати функцію чистою. І він буде правий. Але це було зроблено навмисно, оскільки я хотів зробити цей приклад якомога простішим, і сподіваюся, що мені вдалося це зробити.

![image](https://github.com/UniBreakfast/return-vs-side-effect/assets/19654456/7e21353d-9bbf-4f65-95c3-112f1aa9e219)
