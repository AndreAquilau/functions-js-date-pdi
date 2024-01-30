# functions-js-date-pdi

Funções de data para usar no Apache Pentaho

```js
function formatDate(cDate, cMask) {
  const dia = substr(cDate, 8, 2);
  const mes = substr(cDate, 5, 2);
  const ano = substr(cDate, 0, 4);

  switch (cMask) {
    case "dd/MM/yyyy": {
      dDate = dia + "/" + mes + "/" + ano;
      break;
    }
    case "yyyy-MM-dd": {
      dDate = ano + "-" + mes + "-" + dia;
      break;
    }
    default: {
      dDate = dia + "/" + mes + "/" + ano;
      break;
    }
  }

  return dDate;
}

function primeiroDiaUtilMes(data) {
  const ano = year(data);
  const mes = month(data);
  var primeiroDia = new Date(ano, mes, 1);

  // verifica se o primeiro dia é sábado ou domingo
  while (primeiroDia.getDay() == 0 || primeiroDia.getDay() == 6) {
    // adiciona um dia
    primeiroDia.setDate(primeiroDia.getDate() + 1);
  }

  return date2str(primeiroDia, "yyyy-MM-dd");
}

function ultimoDiaUtilMes(data) {
  const ano = year(data);
  const mes = month(data);
  var ultimoDia = new Date(ano, mes + 1, 0);

  // verifica se o último dia é sábado ou domingo
  while (ultimoDia.getDay() == 0 || ultimoDia.getDay() == 6) {
    // subtrai um dia
    ultimoDia.setDate(ultimoDia.getDate() - 1);
  }

  return date2str(ultimoDia, "yyyy-MM-dd");
}

function primeiroDiaUtilMesAnterior(data) {
  const ano = year(data);
  const mes = month(data);
  var primeiroDia = new Date(ano, mes, 1);

  primeiroDia = dateAdd(primeiroDia, "m", -1);

  // verifica se o primeiro dia é sábado ou domingo
  while (primeiroDia.getDay() == 0 || primeiroDia.getDay() == 6) {
    // adiciona um dia
    primeiroDia.setDate(primeiroDia.getDate() + 1);
  }

  return date2str(primeiroDia, "yyyy-MM-dd");
}

function ultimoDiaUtilMesAnterior(data) {
  const ano = year(data);
  const mes = month(data);
  var ultimoDia = new Date(ano, mes + 1, 0);

  ultimoDia = dateAdd(ultimoDia, "m", -1);

  // verifica se o último dia é sábado ou domingo
  while (ultimoDia.getDay() == 0 || ultimoDia.getDay() == 6) {
    // subtrai um dia
    ultimoDia.setDate(ultimoDia.getDate() - 1);
  }

  return date2str(ultimoDia, "yyyy-MM-dd");
}

function ProximoDiaUtilData(data) {
  const auxDate = data;
  const day = getDayNumber(auxDate, "w");

  if (day == 5) {
    auxDate.setDate(auxDate.getDate() + 3);
  } else if (day == 6) {
    auxDate.setDate(auxDate.getDate() + 2);
  } else {
    auxDate.setDate(auxDate.getDate() + 1);
  }

  return date2str(auxDate, "yyyy-MM-dd");
}

function DiaUtilData(data) {
  const auxDate = data;
  const day = getDayNumber(auxDate, "w");

  if (day == 0) {
    auxDate.setDate(auxDate.getDate() - 2);
  } else if (day == 6) {
    auxDate.setDate(auxDate.getDate() - 1);
  }

  return date2str(auxDate, "yyyy-MM-dd");
}

function SoNumeros(text) {
  return getDigitsOnly(text);
}

function SomaDias(data, dias) {
  const soma = dateAdd(data, "d", dias);
  return date2str(soma, "yyyy-MM-dd");
}

var data = formatDate(date, "yyyy-MM-dd");
var dataPrimeiroDiaUtilMes = primeiroDiaUtilMes(str2date(data, "yyyy-MM-dd"));
var dataUltimoDiaUtilMes = ultimoDiaUtilMes(str2date(data, "yyyy-MM-dd"));
var dataPrimeiroDiaUtilMesAnterior = primeiroDiaUtilMesAnterior(
  str2date(data, "yyyy-MM-dd")
);
var dataUltimoDiaUtilMesAnterior = ultimoDiaUtilMesAnterior(
  str2date(data, "yyyy-MM-dd")
);
var dataProximoDiaUtilData = ProximoDiaUtilData(str2date(data, "yyyy-MM-dd"));
var dataDiaUtilData = DiaUtilData(str2date(data, "yyyy-MM-dd"));
var dataSoma90Dias = SomaDias(str2date(data, "yyyy-MM-dd"), 90);
```
