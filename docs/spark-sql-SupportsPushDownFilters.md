title: SupportsPushDownFilters

# SupportsPushDownFilters -- Data Source Readers with Filter Pushdown Optimization Support

`SupportsPushDownFilters` is the <<contract, extension>> of the <<spark-sql-DataSourceReader.md#, DataSourceReader contract>> for <<implementations, data source readers>> in [DataSource V2](new-and-noteworthy/datasource-v2.md). that support <<pushedFilters, filter pushdown>> performance optimization (and hence reduce the size of the data to be read).

[[contract]]
.SupportsPushDownFilters Contract
[cols="1m,3",options="header",width="100%"]
|===
| Method
| Description

| pushedFilters
a| [[pushedFilters]]

[source, java]
----
Filter[] pushedFilters()
----

<<spark-sql-Filter.md#, Data source filters>> that were pushed down to the data source (in <<pushFilters, pushFilters>>)

Used exclusively when [DataSourceV2Strategy](execution-planning-strategies/DataSourceV2Strategy.md) execution planning strategy is executed (on a [DataSourceV2Relation logical operator](execution-planning-strategies/DataSourceV2Strategy.md#apply-DataSourceV2Relation) with a `SupportsPushDownFilters` reader)

| pushFilters
a| [[pushFilters]]

[source, java]
----
Filter[] pushFilters(Filter[] filters)
----

<<spark-sql-Filter.md#, Data source filters>> that need to be evaluated again after scanning (so Spark can plan an extra filter operator)

Used exclusively when [DataSourceV2Strategy](execution-planning-strategies/DataSourceV2Strategy.md) execution planning strategy is executed (on a [DataSourceV2Relation logical operator](execution-planning-strategies/DataSourceV2Strategy.md#apply-DataSourceV2Relation) with a `SupportsPushDownFilters` reader)

|===

[NOTE]
====
`SupportsPushDownFilters` is an `Evolving` contract that is evolving towards becoming a stable API, but is not a stable API yet and can change from one feature release to another release.

In other words, using the contract is as treading on thin ice.
====
