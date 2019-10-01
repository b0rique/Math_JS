 // Эта функция выполняет разбор числа, переводя его в компоненты — знак, целочисленный коэффициент и экспоненту:
function deconstruct(number) {

    let sign = 1;
    let coefficient = number;
    let exponent = 0; 
    number = sign * coefficient * (2 ** exponent);
// Убираем знак из коэффициента:
if (coefficient < 0) {
    coefficient = -coefficient;
    sign = -1;
}
// Выполняем перевод коэффициента: 
// получить экспоненту можно делением 
// числа на 2 до тех пор, пока не будет получен нуль. 
// Количество делений добавляем к –1128, 
// то есть к экспоненте Number.MIN_VALUE за вычетом 
// количества разрядов в значимой части числа и бонусного разряда: 

if (Number.isFinite(number) && number != 0) {
    exponent = -1128; 
    let reduction = coefficient;
    while (reduction != 0) {
// Этот цикл гарантирует достижения нуля. 
// Каждая операция деления будет уменьшать экспоненту перевода. 
// Когда она станет настолько малой, что ее невозможно будет уменьшить на единицу, 
// тогда вместо этого внутренняя субнормальная значимая часть будет сдвинута вправо. 
// В конечном итоге будут удалены все разряды: 
        exponent += 1;
        reduction /= 2;
        }
        reduction = exponent;

        while(reduction > 0) {
            coefficient /= 2;
            reduction -=1;
        }
        while(reduction < 0) {
            coefficient *= 2;
            reduction += 1;
        }
    }
// Возвращаем объект, содержащий три компонента и исходное число: 
    return {
        sign,
        coefficient,
        exponent,
        number
    

 
    }; 

}
            
deconstruct(1);
           
    console.log(number);
  
