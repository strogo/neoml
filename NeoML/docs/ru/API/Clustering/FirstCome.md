# По первому пришедшему CFirstComeClustering

<!-- TOC -->

- [По первому пришедшему CFirstComeClustering](#по-первому-пришедшему-cfirstcomeclustering)
	- [Параметры](#параметры)
	- [Пример](#пример)

<!-- /TOC -->

Это простой алгоритм кластеризации, работающий за один проход по набору данных. Для каждого нового вектора из набора либо создается новый кластер, если он достаточно далеко от существующих, либо вектор добавляется в ближайший из существующих кластеров. В конце работы слишком маленькие кластера (число элементов меньше *MinClusterSizeRatio*) разрушаются, а их вектора перераспределяются.

В **NeoML** алгоритм реализован классом `CFirstComeClustering`, который предоставляет интерфейс `IClustering`. Кластеризация производится с помощью его метода `Clusterize`.

## Параметры

Параметры кластеризации описываются структурой `CFirstComeClustering::CParam`.

- *DistanceFunc* — используемая функция растояния;
- *MinVectorCountForVariance* — минимальное количество векторов в кластере, при котором дисперсия считается приемлемой;
- *DefaultVariance* — дисперсия по умолчанию (в случае, когда число элементов в кластере меньше *MinVectorCountForVariance*);
- *Threshold* — порог расстояния для создания нового кластера;
- *MinClusterSizeRatio* — минимально допустимое количество элементов в кластере (доля относительно общего числа векторов, значения от 0 до 1);
- *MaxClusterCount* — максимально допустимое количество кластеров (используется для того, чтобы алгоритм не создал слишком много кластеров для данных с большим разбросом).

## Пример

В данном примере алгоритм по первому пришедшему используется для кластеризации набора данных [Iris Data Set](http://archive.ics.uci.edu/ml/datasets/Iris):

```c++
void Clusterize( IClusteringData& irisDataSet, CClusteringResult& result )
{
	CFirstComeClustering::CParam params;
	params.Threshold = 5;

	CFirstComeClustering firstCome( params );
	firstCome.Clusterize( irisDataSet, result );
}
```