# 单位工厂交互行为分析

## 当前情况

1. **类继承关系**：
   - `DerivativeUnitFactory` 继承自 `UnitFactory`（Mindustry内置单位工厂类）
   - `DerivativeBuild` 继承自 `UnitFactoryBuild`（UnitFactory的建造物类）

2. **交互行为**：
   - 由于继承了 `UnitFactory`，工厂会保留默认的交互行为
   - 玩家点击工厂时，会出现交互界面
   - 但是，交互列表会是空的，因为没有添加任何可生产的单位计划

3. **原因**：
   - 在 `CustomUnitMod.java` 中，创建了 `DerivativeUnitFactory` 实例，但没有添加任何 `UnitPlan`
   - `UnitFactory` 的交互列表只会显示已添加到 `plans` 列表中的单位计划

## 如何添加可生产的单位

要让玩家点击工厂时显示可交互的单位列表，需要添加 `UnitPlan` 到