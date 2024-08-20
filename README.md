[25/08/2023 11:24] Eduardo de Oliveira, Kleber
sim correto
 
[25/08/2023 11:26] Eduardo de Oliveira, Kleber
estas são as query's mais usadas do lado Sinacor para buscar os tempos e volumes
 
[25/08/2023 11:26] Eduardo de Oliveira, Kleber
select '01.Recepcao de Execucoes' ACAO, case x.cod_trat_flux when 1 then 'Admincon' when 4 then 'HFT' when 3 then 'Default' else 'Derivativos' end ITEM, to_char(y.tmst_neg_det, 'DD/MM/YYYY HH24:MI') HORARIO, count(*) TOTAL from tmorneg_det y, tmorcasd z, tmororde x where trunc(tmst_neg_det) >= trunc(sysdate) and y.num_seq_neg = z.num_seq_neg and z.num_seq_orde = x.num_seq_orde group by x.cod_trat_flux, to_char(y.tmst_neg_det, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
select '02.Mensagens Capturadas' ACAO, cod_idt_msg ITEM, to_char (tmst_incl, 'DD/MM/YYYY HH24:MI') HORARIO, count(1) TOTAL from taum_msg_rcpc WHERE TMST_INCL >= to_char(sysdate) group by cod_idt_msg, to_char(tmst_incl, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
select '02.Mensagens Recepcionadas Captura' ACAO, cod_idt_msg ITEM, to_char(tmst_incl, 'DD/MM/YYYY HH24:MI') HORARIO, count(1) TOTAL from TAUM_MSG_RCPC_CAPT WHERE TMST_INCL >= trunc(sysdate) group by cod_idt_msg, to_char(tmst_incl, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
select '02.Mensagens Recepcionadas Alocacao' ACAO, cod_idt_msg ITEM, to_char(tmst_incl, 'DD/MM/YYYY HH24:MI') HORARIO, count(1) TOTAL from TAUM_MSG_RCPC_ALOC WHERE TMST_INCL >= trunc(sysdate) group by cod_idt_msg, to_char(tmst_incl, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
select '03.Negocios Capturados' ACAO, 'EQUITIES' ITEM, to_char(tmst_incl, 'DD/MM/YYYY HH24:MI') HORARIO, count(1) TOTAL from TAUM_NEG_REG where cod_segm = 1 and tmst_incl >= to_char(sysdate) group by to_char(tmst_incl, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
select '03.Negocios Capturados' ACAO, 'DERIVATIVOS' ITEM, to_char(tmst_incl, 'DD/MM/YYYY HH24:MI') HORARIO, count(1) TOTAL from TAUM_NEG_REG where cod_segm = 5 and tmst_incl >= to_char(sysdate) group by to_char(tmst_incl, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
select '04.Negocios Processados' ACAO, 'EQUITIES' ITEM, to_char(tmst_neg_det, 'DD/MM/YYYY HH24:MI') HORARIO, count(1) TOTAL from tmorneg_det where tmst_neg_det >= to_char(sysdate) group by to_char(tmst_neg_det, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
select '04.Negocios Processados' ACAO, 'DERIVATIVOS' ITEM, to_char(dt_stamp, 'DD/MM/YYYY HH24:MI') HORARIO, count(1) TOTAL from tmfnegos fn where tp_registro = 1 and dt_stamp >= to_char(sysdate) group by to_char(dt_stamp, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
select '05.Negocios Especificados' ACAO, 'EQUITIES' ITEM, to_char(dthr_esp, 'DD/MM/YYYY HH24:MI') HORARIO, count(1) TOTAL from tmoresp where dthr_esp >= to_char(sysdate) group by to_char(dthr_esp, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
select '06.Repasses Recebidos' ACAO, 'BVMF.019' ITEM, to_char(tmst_incl, 'DD/MM/YYYY HH24:MI') HORARIO, COUNT(1) TOTAL from Taum_Rpss where tmst_incl >= to_char(sysdate) group by to_char(tmst_incl, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
select '07.Envio p/ B3' ACAO, cod_tipo_iso ITEM, to_char(data_env_msg, 'DD/MM/YYYY HH24:MI') HORARIO, count(1) TOTAL from taum_msg_env where data_env_msg >= to_char(sysdate) group by cod_tipo_iso, to_char(data_env_msg, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
select '08.Integracao' ACAO, 'Negócios' ITEM, to_char(DT_SISTEMA, 'DD/MM/YYYY HH24:MI') HORARIO, count(1) TOTAL from tornegd where dt_pregao >= to_char(sysdate) group by to_char(DT_SISTEMA, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
select '08.Integracao' ACAO, 'Ordens' ITEM, to_char(DT_SISTEMA, 'DD/MM/YYYY HH24:MI') HORARIO, count(1) TOTAL from tormovd where trunc(dt_sistema) >= trunc(sysdate) group by to_char(DT_SISTEMA, 'DD/MM/YYYY HH24:MI') order by 3 asc ;
 
select '09. Ordens abertas' ACAO, 'EQUITIES' ITEM, to_char(dthr_reg_orde, 'DD/MM/YYYY HH24:MI') HORARIO, COUNT(1) from TMORORDE WHERE dthr_reg_orde >= to_char(sysdate) group BY to_char(dthr_reg_orde, 'DD/MM/YYYY HH24:MI') order by 3 asc;
 
--Coleta quantidade de clientes negociando no dia BOV - dia 15/09
select count(distinct d.cod_idt_con_cli)
from corrwin.tmorneg n, corrwin.tmorneg_Det d
where n.data_preg = to_date('20221003', 'YYYYMMDD')
and d.num_seq_neg = n.num_seq_neg;
--Coleta quantidade de clientes negociando no dia BMF - dia 15/09
select count(distinct bmf.cd_cliente) from corrwin.tmfnegos bmf
where bmf.dt_pregao = to_date('20221003', 'YYYYMMDD')
and bmf.tp_registro = 1;
 
 
--Coleta quantidade de clientes negociando no dia BOV - dia 16/09
select count(distinct d.cod_idt_con_cli)
from corrwin.tmorneg n, corrwin.tmorneg_Det d
where n.data_preg = to_date('20220916', 'YYYYMMDD')
and d.num_seq_neg = n.num_seq_neg;
--Coleta quantidade de clientes negociando no dia BMF - dia 16/09
select count(distinct bmf.cd_cliente) from corrwin.tmfnegos bmf
where bmf.dt_pregao = to_date('20221003', 'YYYYMMDD')
and bmf.tp_registro = 1;
