-- Selecionar as colunas:
-- organization_state state da tabela organizations
-- organization_industry da tabela organizations
-- order_date da tabela orders
-- order_value da tabela orders
-- contract_marketplace da tabela contracts

-- order_value entre 10k e 100k
-- order_date últimos 90 dias
-- order_state

-- order_id, order_date, order_value, material_liability, liability_location, order_status

--SQLite 3
SELECT 
ord.organization_id_fk as organization_id,
ord.contract_id_fk as contract_id,
ord.order_value as valor,
ord.order_status as status_pedido,
ord.order_date as data_pedido,
orga.organization_state as estado, 
cont.contract_marketplace as tipo_contrato, 
orga.organization_industry as industria
FROM orders AS ord
INNER JOIN organizations AS orga on ord.organization_id_fk = orga.organization_id_pk
INNER JOIN contracts AS cont on ord.contract_id_fk = cont.contract_id_pk
WHERE ord.order_date >= DATEADD(DAY, -90, GETDATE()) --últimos 90 dias, verificar versão do SQL // tentar WHERE ord.order_date >= date('now', '-90 day')
AND ord.order_value BETWEEN 10000.00 AND 100000.00
ORDER BY orga.organization_state, cont.contract_marketplace, orga.organization_industry;


