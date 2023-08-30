# Forex
//+------------------------------------------------------------------+
//|                                                ClaricaSantos.mq5 |
//|                                  Copyright 2023, MetaQuotes Ltd. |
//|                                             https://www.mql5.com |
//+------------------------------------------------------------------+
#property copyright "Copyright 2023, MetaQuotes Ltd."
#property link      "https://www.mql5.com"
#property version   "1.00"

struct s_position
  {
   double            volume;
   double            lucro;
   ulong             ticket;
   double            sl;
   double            tp;
   datetime          hora;
  };

struct s_ordem
  {
   ulong             af1;
   ulong             af2;
   ulong             af3;
   ulong             af4;
   ulong             af5;
   ulong             ac1;
   ulong             ac2;
   ulong             ac3;
   ulong             ac4;
   ulong             ac5;
   ulong             p1;
   ulong             p2;
   ulong             p3;
   ulong             p4;
   ulong             buy;
   ulong             sell;
   ulong             out;
  };

struct s_history
  {
   datetime          ult_time;
   double            entrada;
   double            medio;
   double            saldo;
   double            max;
   double            min;
   double            saldo_dia;
   double            saldo_sem;
   double            saldo_mes;
   double            saldo_total;
   int               cnt_dia;
   int               cnt_sem;
   int               cnt_mes;
   int               cnt_total;
   int               gains_dia;
   int               gains_sem;
   int               gains_mes;
   int               gains_total;
   ulong             af1;
   ulong             af2;
   ulong             af3;
   ulong             af4;
   ulong             af5;
   ulong             ac1;
   ulong             ac2;
   ulong             ac3;
   ulong             ac4;
   ulong             ac5;
   ulong             p1;
   ulong             p2;
   ulong             p3;
   ulong             p4;
   ulong             last;
  };

enum e_tempo
  {
   es_s = 0, // Segundos
   es_m = 1, // Minutos
   es_h = 2, // Horas
   es_v = 3 // Velas
  };

enum e_meta
  {
   es_off = 0, // Desabilitado
   es_dia = 1, // Meta diária
   es_sem = 2, // Meta Semanal
   es_mes = 3 // Meta Mensal
  };

enum e_sn
  {
   es_nao = 0, // Não
   es_sim = 1 // Sim
  };

enum e_pro
  {
   es_tick = 0, // Cada tick
   es_seg = 1 // Cada segundo
  };

enum e_hr
  {
   eh_00 = 0,    // 00h
   eh_01 = 1,    // 01h
   eh_02 = 2,    // 02h
   eh_03 = 3,    // 03h
   eh_04 = 4,    // 04h
   eh_05 = 5,    // 05h
   eh_06 = 6,    // 06h
   eh_07 = 7,    // 07h
   eh_08 = 8,    // 08h
   eh_09 = 9,    // 09h
   eh_10 = 10,   // 10h
   eh_11 = 11,   // 11h
   eh_12 = 12,   // 12h
   eh_13 = 13,   // 13h
   eh_14 = 14,   // 14h
   eh_15 = 15,   // 15h
   eh_16 = 16,   // 16h
   eh_17 = 17,   // 17h
   eh_18 = 18,   // 18h
   eh_19 = 19,   // 19h
   eh_20 = 20,   // 20h
   eh_21 = 21,   // 21h
   eh_22 = 22,   // 22h
   eh_23 = 23    // 23h
  };

enum e_min
  {
   em_00 = 0,    // 00m
   em_01 = 1,    // 01m
   em_02 = 2,    // 02m
   em_03 = 3,    // 03m
   em_04 = 4,    // 04m
   em_05 = 5,    // 05m
   em_06 = 6,    // 06m
   em_07 = 7,    // 07m
   em_08 = 8,    // 08m
   em_09 = 9,    // 09m
   em_10 = 10,   // 10m
   em_11 = 11,   // 11m
   em_12 = 12,   // 12m
   em_13 = 13,   // 13m
   em_14 = 14,   // 14m
   em_15 = 15,   // 15m
   em_16 = 16,   // 16m
   em_17 = 17,   // 17m
   em_18 = 18,   // 18m
   em_19 = 19,   // 19m
   em_20 = 20,   // 20m
   em_21 = 21,   // 21m
   em_22 = 22,   // 22m
   em_23 = 23,   // 23m
   em_24 = 24,   // 24m
   em_25 = 25,   // 25m
   em_26 = 26,   // 26m
   em_27 = 27,   // 27m
   em_28 = 28,   // 28m
   em_29 = 29,   // 29m
   em_30 = 30,   // 30m
   em_31 = 31,   // 31m
   em_32 = 32,   // 32m
   em_33 = 33,   // 33m
   em_34 = 34,   // 34m
   em_35 = 35,   // 35m
   em_36 = 36,   // 36m
   em_37 = 37,   // 37m
   em_38 = 38,   // 38m
   em_39 = 39,   // 39m
   em_40 = 40,   // 40m
   em_41 = 41,   // 41m
   em_42 = 42,   // 42m
   em_43 = 43,   // 43m
   em_44 = 44,   // 44m
   em_45 = 45,   // 45m
   em_46 = 46,   // 46m
   em_47 = 47,   // 47m
   em_48 = 48,   // 48m
   em_49 = 49,   // 49m
   em_50 = 50,   // 50m
   em_51 = 51,   // 51m
   em_52 = 52,   // 52m
   em_53 = 53,   // 53m
   em_54 = 54,   // 54m
   em_55 = 55,   // 55m
   em_56 = 56,   // 56m
   em_57 = 57,   // 57m
   em_58 = 58,   // 58m
   em_59 = 59    // 59m
  };

enum e_price
  {
   es_mercado = 0, // Preço de mercado
   es_max = 1, // Máxima atual
   es_min = 2, // Mínima atual
   es_open = 3, // Abertura atual
   es_last_max = 4, // Máxima anterior
   es_last_min = 5, // Mínima anterior
   es_close = 6, // Fechamento anterior
   es_3_max = 7, // Máxima dos 3 últimos
   es_3_min = 8, // Mínima dos 3 últimos
   es_day_max = 9, // Máxima do dia
   es_day_min = 10, // Mínima do dia
   es_day_open = 11, // Abertura do dia
   es_day_last_max = 12, // Máxima dia anterior
   es_day_last_min = 13, // Mínima dia anterior
   es_day_last_close = 14 // Fechamento dia anterior
  };

enum e_mercado
  {
   es_b3 = ORDER_FILLING_RETURN, // B3
   es_forex = ORDER_FILLING_FOK // Forex
  };

enum e_validade
  {
   es_swing = ORDER_TIME_GTC, // Swing Trade
   es_day = ORDER_TIME_DAY // Day Trade
  };

enum e_semana
  {
   es_diariamente = 0, // Todos os dias
   es_segunda = 1, // Segundas
   es_terca = 2, // Terças
   es_quarta = 3, // Quartas
   es_quinta = 4, // Quintas
   es_sexta = 5, // Sextas
   es_sabado = 6 // Sábados
  };

enum e_buys_in
  {
   es_buy_in_1 = 0, // Sinal entrada compra 1
   es_buy_in_2 = 1, // Sinal entrada compra 2
   es_buy_in_3 = 2 // Sinal entrada compra 3
  };

enum e_sells_in
  {
   es_sell_in_1 = 0, // Sinal entrada venda 1
   es_sell_in_2 = 1, // Sinal entrada venda 2
   es_sell_in_3 = 2 // Sinal entrada venda 3
  };

enum e_buys_out
  {
   es_buy_out_1 = 0, // Sinal saída compra 1
   es_buy_out_2 = 1, // Sinal saída compra 2
   es_buy_out_3 = 2 // Sinal saída compra 3
  };

enum e_sells_out
  {
   es_sell_out_1 = 0, // Sinal saída venda 1
   es_sell_out_2 = 1, // Sinal saída venda 2
   es_sell_out_3 = 2 // Sinal saída venda 3
  };
//+------------------------------------------------------------------+
class GLOBAL
  {
protected:
   string                  _prefix_painel, _prefix_linha;
   ENUM_ORDER_TYPE_TIME    _validade;
   ENUM_ORDER_TYPE_FILLING _filling;
   MqlDateTime             _time_inicio, _time_parar, _time_zerar, _time_corrente;
   bool                    _comprar, _vender, _repo_sl, _repo_tp, _block_in, _block_out, _cancel_oposto;
   int                     _handle_1, _handle_2, _handle_3, _handle_4;
   int                     _handle_5, _handle_6, _handle_7, _handle_8;
   double                  _medio_tp, _medio_sl, _medio_pn;
   bool                    _pts_inout, _pts_cus, _pts_tp, _pts_sl, _pts_ac, _pts_af, _pts_pn, _ajustar, _pts_grad;
   double                  _boleta;
   ulong                   _contas[4], _permitidas;
   datetime                _expiracao;
   bool                    _back, _demo, _contest, _real;
   int                     _max_buy_in, _max_buy_out, _max_sell_in, _max_sell_out, _vol_digitos;

public:
   bool                    _operar, _minimizado, _atualizar, _visual, _teste;
   string                  set_simbolo(void);
   bool                    verificar_licenca(void);
  };
//+------------------------------------------------------------------+
class GRAFICO : public GLOBAL
  {
private:
   struct s_local
     {
      bool           mover;
      bool           confirmado;
      string         linha;
      string         etiqueta;
      ulong          ticket;
     };

   s_local           _tarja;
   string            _linhas[15];

protected:
   void              update_painel_position(const s_position &pos);
   color             confirmar_cor(const double valor);
   void              set_obj(const ENUM_OBJECT obj, const string nome, const int lat_dis, const int top_dis, const int larg,
                             const int alt, const int width, const color clr_fundo, const color clr_borda,
                             const string font, const int font_size, const string txt, const color clr_txt,
                             const bool press=false);
   void              update_painel_descritivo(const string msg);
   void              set_grafico(void);
   void              filtro_log(const string msg);
   bool              criar_painel(void);
   bool              minimizar_painel(void);
   void              excluir_indicadores(void);
   void              update_painel_history(const s_history &his);
   void              gerenciar_linhas(const s_position &pos, const s_ordem &ord, const ulong &grad[], const double entrada, const double medio);
   bool              criar_linha(const string nome, const ulong ticket, const string txt, const double price, const color cor,
                                 const ENUM_LINE_STYLE style, const double saldo=0, const bool botao=true);
   bool              modificar_linha(const string nome, const string etiqueta, const ulong ticket, const bool remover);
   void              processar_boleta(const string botao);
   bool              criar_log(void);

public:
   void              processar_grafico(const int id, const long lparam, const double dparam, const string sparam);
  };
//+------------------------------------------------------------------+
class CONTROLE : public GRAFICO
  {
protected:
   void              check_windows(const int &window[]);
   bool              check_metas(const double saldo, const double lucro, const double max, const double min);
   s_history         historico(int &grad_qtd[], const datetime abertura=0);
   s_ordem           ordens(ulong &grad_ticket[], const datetime abertura, const double pos_tp=0, const double pos_sl=0);
   bool              check_conexao(void);
   bool              check_volume_inicial(const double volume);
   bool              check_volumes(void);
   bool              check_indicadores(void);
   bool              check_ticks(void);
   bool              check_ativo(void);
   void              check_globais(void);
   void              check_visual(void);
   bool              check_filling(const ENUM_TRADE_REQUEST_ACTIONS action, ENUM_ORDER_TYPE_FILLING &filling);
   bool              check_expiration(ENUM_ORDER_TYPE_TIME &time);
   bool              check_espera(const datetime time, const int espera);
   bool              check_temporizador(const datetime time, const int espera, const e_tempo referencia);
   void              iniciar_handles(void);

public:
   s_position        posicao(void);
   void              check_buffers(void);
  };
//+------------------------------------------------------------------+
class HORARIO : public CONTROLE
  {
protected:
   bool              check_barra(const bool candle_out, const datetime time);
   void              set_horario(void);

public:
   bool              horario_operacional(void);
   bool              horario_zeragem(void);
   void              atualizar_hora(void);
   bool              horario_espera(void);
  };
//+------------------------------------------------------------------+
class EXECUCAO : public HORARIO
  {
protected:
   double            check_conversao(const bool pts, const double valor, const double price=0.0);
   bool              check_sentido(const double valor1, const double valor2, const int sentido);
   bool              check_sinal(int &sinal, const int menu1, const double value1, const int coef1, const double var1,
                                 const int sentido, const int menu2, const double value2, const int coef2, const double var2);
   double            check_coeficiente(const double valor, const int coef, const double var);
   bool              trailling_tp(const ulong ticket, const double price);
   bool              breakeven_tp(const ulong ticket, const double price);
   bool              trailling_sl(const ulong ticket, const double price);
   bool              breakeven_sl(const ulong ticket, const double price);
   bool              check_stoplevel(double &price, const ENUM_ORDER_TYPE tipo, const bool corrigir=false, const double ajustar=0.00);
   bool              check_permissao(void);
   bool              check_spread(void);
   double            check_price(const e_price pr);
   bool              check_saida_venda(void);
   bool              check_entrada_venda(void);
   bool              check_saida_compra(void);
   bool              check_entrada_compra(void);
   bool              check_canais_compra_in(int &sinal);
   bool              check_canais_venda_in(int &sinal);
   bool              check_canais_compra_out(int &sinal);
   bool              check_canais_venda_out(int &sinal);
   bool              check_oscilar_compra_in(int &sinal);
   bool              check_oscilar_venda_in(int &sinal);
   bool              check_oscilar_compra_out(int &sinal);
   bool              check_oscilar_venda_out(int &sinal);
   bool              check_cruzar_compra_in(int &sinal);
   bool              check_cruzar_venda_in(int &sinal);
   bool              check_cruzar_compra_out(int &sinal);
   bool              check_cruzar_venda_out(int &sinal);
   bool              check_alvos(const double pos, const ulong ticket, const double primeira, const double medio);
   bool              enviar_venda(void);
   bool              enviar_compra(void);
   bool              enviar_saida(const double pos, const ulong ticket_out);
   bool              check_gradiente_linear(const double posicao, const double entrada, const int &grad_qtd[], const ulong &grad_ticket[], const ulong last, const double sl);
   bool              check_pendentes(const s_position &pos, const s_ordem &ord, const s_history &his);
   void              confirmar_aumento(const bool contra, const double pos, const double entrada, const double sl, const double tp,
                                       const double dis, const double lot, const ulong ticket, const ulong history, const string nome);
   void              confirmar_parciais(const double pos, const double price, const double dis, const double lot,
                                        const ulong ticket, const ulong history, const string nome);
   bool              check_saida_temporal(const datetime hora, const double lucro);
   bool              check_filtro_barra(void);
   bool              check_procura_sinal(const bool compra, const bool saida, const datetime ultima);

public:
   double            normalizar(const double price);
   void              zeragem_compulsoria(void);
   bool              enviar_ordem(const ENUM_TRADE_REQUEST_ACTIONS action, const ENUM_ORDER_TYPE tipo,
                                  double price=0, ulong  ticket=0, double tp=0, double sl=0, double lot=0, string coment=NULL, ulong ticket_by=0);
  };
//+------------------------------------------------------------------+
class PROCESSAR : public EXECUCAO
  {
private:
   void              processar_zerado(const s_history &his, ulong &grad_ticket[]);
   void              processar_posicionado(const s_position &pos, const s_ordem &ord, const s_history &his, const int &grad_qtd[], const ulong &grad_ticket[]);

public:
   bool              iniciando(void);
   void              desligando(void);
   void              processando(void);
  };
//+------------------------------------------------------------------+
PROCESSAR in_pro;
//+------------------------------------------------------------------+
#define Robot "OlimBot_1693176862"
#define Expert "FastOperation03"
#property description "Expert Advisor FastOperation03"
#property description "Criado com o construtor OlimBot em 27/08/2023 - 19:54:22"

sinput group "--- PARAMETRIZAÇÃO INICIAL ---"
sinput ulong m_magic = 1693176862; // Magic Number (ID)
sinput e_pro m_processo = es_tick; // Modo de processamento
sinput e_mercado m_mercado = (e_mercado)ORDER_FILLING_FOK; // Tipo de mercado
sinput e_validade m_validade = (e_validade)ORDER_TIME_GTC; // Modo operacional

sinput group "--- CONFIGURAÇÃO ADICIONAL ---"
input ENUM_TIMEFRAMES m_timeframe = PERIOD_CURRENT; // Tempo gráfico
sinput double m_volume = 0.1; // Volume
sinput int m_spread = 50; // Spread máximo

sinput group "--- CONFIRMAÇÃO DE SINAIS ---"
sinput string m_set = "Setup Padrão"; // Nome do setup
sinput e_buys_in m_compra_in = 0; // Sinal entrada compra
sinput e_sells_in m_venda_in = 0; // Sinal entrada venda
sinput e_buys_out m_compra_out = 0; // Sinal saída compra
sinput e_sells_out m_venda_out = 0; // Sinal saída venda

sinput e_sn m_inverte_in = false; // Inverter sinais de entrada
sinput e_sn m_inverte_out = false; // Inverter sinais de saída

sinput group "--- CROSS ORDER ---"
sinput e_sn m_cross_order = false; // Envio de ordens em outro ativo
sinput string m_cross_ativo = " "; // Ativo para cross order

sinput group "--- COMPLEMENTOS ---"
input e_sn m_sinais_in = false; // Procurar entrada na vela seguinte à saída
input e_sn m_sinais_out = false; // Procurar saída na vela seguinte à entrada

sinput group "--- TEMPORIZAÇÃO ---"
input e_tempo m_espera_ref = 0; // Referência de tempo
input int m_espera_in = 0; // Tempo para nova entrada
input int m_espera_out = 0; // Tempo mínimo de posição

sinput group "--- ORDENS PENDENTES DE ENTRADA ---"
input e_sn m_pendente_in = false; // Ordem pendente p/ entrada
input int m_cancel_in = 0; // Expiração entradas (seg)
input double m_dis_in = 0; // Distância entrada (pts)
input e_price m_price_buy = 0; // Preço p/ compra
input e_price m_price_sell = 0; // Preço p/ venda

sinput group "--- ORDENS PENDENTES DE SAÍDA ---"
input e_sn m_pendente_out = false; // Ordem pendente p/ saída
input int m_cancel_out = 0; // Expiração saídas (seg)
input double m_dis_out = 0; // Distância saída (pts)
input e_price m_price_out_buy = 0; // Saída da compra
input e_price m_price_out_sell = 0; // Saída da venda

sinput group "--- STOPLOSS ---"
input double m_sl = 0; // Stop loss (pts)
input e_sn m_alvos_sl2 = false; // Usar stop personalizado
input double m_dis_sl2 = 0; // Distância stoploss (pts)
input e_price m_price_sl2_buy = 0; // Stop personalizado da compra
input e_price m_price_sl2_sell = 0; // Stop personalizado da venda

sinput group "--- TAKEPROFIT ---"
input double m_tp = 0; // Take Profit (pts)
input e_sn m_alvos_tp2 = false; // Usar take personalizado
input double m_dis_tp2 = 0; // Distância takeprofit (pts)
input e_price m_price_tp2_buy = 0; // Take personalizado da compra
input e_price m_price_tp2_sell = 0; // Take personalizado da venda

sinput group "--- MOVIMENTO STOP LOSS ---"
input double m_sl_be = 0; // Início do breakeven SL (pts)
input double m_sl_be_dis = 0; // Distância do breakeven (pts)
input double m_sl_ts = 0; // Trailling stop (pts)
input double m_sl_ts_step = 0; // Passo do trailling stop (pts)

sinput group "--- MOVIMENTO TAKE PROFIT ---"
input double m_tp_be = 0; // Início do breakeven TP (pts)
input double m_tp_be_dis = 0; // Distância do breakeven (pts)
input double m_tp_ts = 0; // Trailling Profit (pts)
input double m_tp_ts_step = 0; // Passo do trailling profit (pts)

sinput group "--- FILTRO DE CANDLE ---"
input ENUM_TIMEFRAMES m_candle_tf = PERIOD_CURRENT; // Tempo gráfico da vela
input int m_candle_min = 0; // Tamanho mínimo da vela (pts)
input int m_candle_max = 0; // Tamanho máximo da vela (pts)
input int m_corpo_min = 0; // Tamanho mínimo do corpo (pts)
input int m_corpo_max = 0; // Tamanho máximo do corpo (pts)

sinput group "--- SAÍDA TEMPORAL ---"
input e_tempo m_temporal_ref = 0; // Referência de tempo
input int m_temporal_pos_time = 0; // Tempo de referência positivo
input double m_temporal_pos_max = 0; // Saldo máximo positivo
input double m_temporal_pos_min = 0; // Saldo mínimo positivo
input int m_temporal_neg_time = 0; // Tempo de referência negativo
input double m_temporal_neg_max = 0; // Saldo máximo negativo
input double m_temporal_neg_min = 0; // Saldo mínimo negativo

sinput group "--- AUMENTOS A FAVOR ---"
input double m_af1_dis = 0; // Distância a favor 1 (pts)
input double m_af1_lot = 0; // Volume a favor 1
input double m_af2_dis = 0; // Distância a favor 2 (pts)
input double m_af2_lot = 0; // Volume a favor 2
input double m_af3_dis = 0; // Distância a favor 3 (pts)
input double m_af3_lot = 0; // Volume a favor 3
input double m_af4_dis = 0; // Distância a favor 4 (pts)
input double m_af4_lot = 0; // Volume a favor 4
input double m_af5_dis = 0; // Distância a favor 5 (pts)
input double m_af5_lot = 0; // Volume a favor 5

sinput group "--- AUMENTOS CONTRA ---"
input double m_ac1_dis = 0; // Distância contra 1 (pts)
input double m_ac1_lot = 0; // Volume contra 1
input double m_ac2_dis = 0; // Distância contra 2 (pts)
input double m_ac2_lot = 0; // Volume contra 2
input double m_ac3_dis = 0; // Distância contra 3 (pts)
input double m_ac3_lot = 0; // Volume contra 3
input double m_ac4_dis = 0; // Distância contra 4 (pts)
input double m_ac4_lot = 0; // Volume contra 4
input double m_ac5_dis = 0; // Distância contra 5 (pts)
input double m_ac5_lot = 0; // Volume contra 5

sinput group "--- SAÍDAS PARCIAIS ---"
input double m_p1_dis = 0; // Distância parcial 1 (pts)
input double m_p1_lot = 0; // Volume parcial 1
input double m_p2_dis = 0; // Distância parcial 2 (pts)
input double m_p2_lot = 0; // Volume parcial 2
input double m_p3_dis = 0; // Distância parcial 3 (pts)
input double m_p3_lot = 0; // Volume parcial 3
input double m_p4_dis = 0; // Distância parcial 4 (pts)
input double m_p4_lot = 0; // Volume parcial 4

sinput group "--- GRADIENTE LINEAR ---"
input int m_grad_qtd = 0; // Quantidade de níveis
input double m_grad_vol = 0; // Volume das ordens
input int m_grad_max = 0; // Limite de entradas
input double m_gra_dis = 0; // Distância do níveis (pts)
input double m_gra_tp = 0; // Alvo parcial do nível (pts)
input double m_grad_ajuste = 0; // Reposicionar ordem parcial (pts)

sinput group "--- METAS DO EXPERT ---"
input e_meta m_refere = es_dia; // Referência
input double m_gain = 0; // Meta de ganho
input e_sn m_gain_out = true; // Zerar no gain durante um trade
input double m_loss = 0; // Limite de perda
input e_sn m_loss_out = true; // Zerar no loss durante um trade
input double m_dd = 0; // Rebaixamento máximo
input e_sn m_dd_out = false; // Zerar no rebaixamento durante um trade
input double m_dd_gat = 0; // Gatilho p/ Rebaixamento
input double m_rec = 0; // Recuperação mínima
input e_sn m_rec_out = false; // Zerar na recuperação durante um trade
input double m_rec_gat = 0; // Gatilho p/ Recuperação

sinput group "--- HORÁRIO INICIAL ---"
input e_hr m_hr_inicio = 0; // Hora inicial
input e_min m_min_inicio = 0; // Minuto inicial

sinput group "--- HORÁRIO FINAL ---"
input e_hr m_hr_final = 22; // Hora final
input e_min m_min_final = 0; // Minuto final

sinput group "--- HORÁRIO ZERAGEM ---"
input e_sn m_zerar = true; // Zerar por horário
input e_hr m_hr_zerar = 23; // Hora zeragem
input e_min m_min_zerar = 0; // Minuto zeragem

sinput group "--- PAUSAS OPERACIONAIS ---"
input e_tempo m_pausa_ref = 0; // Referência de tempo
input e_hr m_pausa_1_hr = 0; // Hora pausa 1
input e_min m_pausa_1_min = 0; // Minuto pausa 1
input e_semana m_pausa_1_dia = 0; // Dia da pausa 1
input int m_pausa_1_tempo = 0; // Duração da pausa 1
input e_hr m_pausa_2_hr = 0; // Hora pausa 2
input e_min m_pausa_2_min = 0; // Minuto pausa 2
input e_semana m_pausa_2_dia = 0; // Dia da pausa 2
input int m_pausa_2_tempo = 0; // Duração da pausa 2

sinput group "--- VISUALIZAÇÃO GRÁFICA ---"
input e_sn m_total = false; // Exibir saldo total
input e_sn m_inserir = true; // Inserir indicadores
input e_sn m_painel = false; // Inserir painel gráfico
input e_sn m_log = false; // Exibir log informativo
input e_sn m_tarjas = false; // Exibir etiquetas nas ordens
input e_sn m_layout = false; // Alterar layout do gráfico

sinput group "--- [1] Média Móvel ---"
input int m_period_1 = 10; // Período
input int m_shift_1 = 0; // Deslocamento
input ENUM_MA_METHOD m_ma_1 = MODE_EMA; // Tipo de média
input ENUM_APPLIED_PRICE m_price_1 = PRICE_CLOSE; // Tipo de Preço

sinput group "--- [2] Média Móvel ---"
input int m_period_2 = 50; // Período
input int m_shift_2 = 0; // Deslocamento
input ENUM_MA_METHOD m_ma_2 = MODE_EMA; // Tipo de média
input ENUM_APPLIED_PRICE m_price_2 = PRICE_CLOSE; // Tipo de Preço

bool CONTROLE::check_indicadores(void) { 
iniciar_handles();
ENUM_TIMEFRAMES tf = (MQLInfoInteger(MQL_TESTER)) ? m_timeframe : _Period;

_handle_1=iMA(_Symbol,tf,m_period_1,m_shift_1,m_ma_1,m_price_1);
if(_handle_1 == INVALID_HANDLE) return false;

_handle_2=iMA(_Symbol,tf,m_period_2,m_shift_2,m_ma_2,m_price_2);
if(_handle_2 == INVALID_HANDLE) return false;

int window[8] = {0,0,-1,-1,-1,-1,-1,-1};
check_windows(window);
return true;}
bool EXECUCAO::check_entrada_compra(void) { int sinal = 0; 

if(check_canais_compra_in(sinal)) if(check_oscilar_compra_in(sinal)) switch(m_compra_in) { case 0:if((check_cruzar_compra_in(sinal)))
 if((check_sinal(sinal,10,1,0,1,8,20,1,0,1) && check_sinal(sinal,10,2,0,1,7,20,2,0,1))) if(sinal > 0) return true; 
break;
 case 1:if((check_cruzar_compra_in(sinal))) if(sinal > 0) return true; 
break;
 case 2:if((check_cruzar_compra_in(sinal))) if(sinal > 0) return true; 
break;
} 

 return false;} 
bool EXECUCAO::check_saida_compra(void) { int sinal = 0; 

if(check_canais_compra_out(sinal)) if(check_oscilar_compra_out(sinal)) switch(m_compra_out) { case 0:if((check_cruzar_compra_out(sinal)))
 if((check_sinal(sinal,10,1,0,1,9,20,1,0,1) && check_sinal(sinal,10,2,0,1,6,20,2,0,1))) if(sinal > 0) return true; 
break;
 case 1:if((check_cruzar_compra_out(sinal))) if(sinal > 0) return true; 
break;
 case 2:if((check_cruzar_compra_out(sinal))) if(sinal > 0) return true; 
break;
} 

 return false;} 
bool EXECUCAO::check_entrada_venda(void) { int sinal = 0; 

if(check_canais_venda_in(sinal)) if(check_oscilar_venda_in(sinal)) switch(m_venda_in) { case 0:if((check_cruzar_venda_in(sinal)))
 if((check_sinal(sinal,10,1,0,1,9,20,1,0,1) && check_sinal(sinal,10,2,0,1,6,20,2,0,1))) if(sinal > 0) return true; 
break;
 case 1:if((check_cruzar_venda_in(sinal))) if(sinal > 0) return true; 
break;
 case 2:if((check_cruzar_venda_in(sinal))) if(sinal > 0) return true; 
break;
} 

 return false;} 
bool EXECUCAO::check_saida_venda(void) { int sinal = 0; 

if(check_canais_venda_out(sinal)) if(check_oscilar_venda_out(sinal)) switch(m_venda_out) { case 0:if((check_cruzar_venda_out(sinal)))
 if((check_sinal(sinal,10,1,0,1,8,20,1,0,1) && check_sinal(sinal,10,2,0,1,7,20,2,0,1))) if(sinal > 0) return true; 
break;
 case 1:if((check_cruzar_venda_out(sinal))) if(sinal > 0) return true; 
break;
 case 2:if((check_cruzar_venda_out(sinal))) if(sinal > 0) return true; 
break;
} 

 return false;} 
bool EXECUCAO::check_canais_compra_in(int &sinal){
 if(sinal >= 0) return true; 

 return false;} 
bool EXECUCAO::check_canais_compra_out(int &sinal){
 if(sinal >= 0) return true; 

 return false;} 
bool EXECUCAO::check_canais_venda_in(int &sinal){
 if(sinal >= 0) return true; 

 return false;} 
bool EXECUCAO::check_canais_venda_out(int &sinal){
 if(sinal >= 0) return true; 

 return false;} 
bool EXECUCAO::check_oscilar_compra_in(int &sinal){
 if(sinal >= 0) return true; 

 return false;} 
bool EXECUCAO::check_oscilar_compra_out(int &sinal){
 if(sinal >= 0) return true; 

 return false;} 
bool EXECUCAO::check_oscilar_venda_in(int &sinal){
 if(sinal >= 0) return true; 

 return false;} 
bool EXECUCAO::check_oscilar_venda_out(int &sinal){
 if(sinal >= 0) return true; 

 return false;} 
bool EXECUCAO::check_cruzar_compra_in(int &sinal){
 if(sinal >= 0) return true; 

 return false;} 
bool EXECUCAO::check_cruzar_compra_out(int &sinal){
 if(sinal >= 0) return true; 

 return false;} 
bool EXECUCAO::check_cruzar_venda_in(int &sinal){
 if(sinal >= 0) return true; 

 return false;} 
bool EXECUCAO::check_cruzar_venda_out(int &sinal){
 if(sinal >= 0) return true; 

 return false;} 
void CONTROLE::check_globais(void) { 
_filling = (ENUM_ORDER_TYPE_FILLING)m_mercado;
_validade = (ENUM_ORDER_TYPE_TIME)m_validade;
_comprar = true;
_vender = true;
_pts_inout = true;
_pts_cus = true;
_pts_sl = true;
_pts_tp = true;
_pts_ac = true;
_pts_af = true;
_pts_pn = true;
_pts_grad = true;
_cancel_oposto = false;
_repo_sl = false;
_repo_tp = false;
_medio_sl = false;
_medio_tp = false;
_medio_pn = false;
_block_in = false;
_block_out = false;
_ajustar = false;
_back = true;
_demo = true;
_contest = true;
_real = true;
_permitidas = 0;
_contas[0] = 0;
_contas[1] = 0;
_contas[2] = 0;
_contas[3] = 0;
_expiracao = 0;
_max_buy_in = 1;
_max_buy_out = 1;
_max_sell_in = 1;
_max_sell_out = 1;
}
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool GLOBAL::verificar_licenca(void)
  {
   if(!_back)
      if(MQLInfoInteger(MQL_TESTER) || MQLInfoInteger(MQL_OPTIMIZATION))
        {
         printf("Não é permitido usar este expert em back teste. Contate o desenvolvedor");
         return false;
        }

   ulong conta = AccountInfoInteger(ACCOUNT_LOGIN);
   ENUM_ACCOUNT_TRADE_MODE modo = (ENUM_ACCOUNT_TRADE_MODE)AccountInfoInteger(ACCOUNT_TRADE_MODE);

   switch(modo)
     {
      case ACCOUNT_TRADE_MODE_DEMO:
         if(!_demo)
           {
            printf("Contas demos não são permitidas. Contate o desenvolvedor");
            return false;
           }
         break;
      case ACCOUNT_TRADE_MODE_CONTEST:
         if(!_contest)
           {
            printf("Contas de torneios não são permitidas. Contate o desenvolvedor");
            return false;
           }
         break;
      case ACCOUNT_TRADE_MODE_REAL:
         if(!_real)
           {
            printf("Contas reais não são permitidas. Contate o desenvolvedor");
            return false;
           }
         break;
      default:
         printf("Erro desconhecido na verificação da licença");
         return false;
         break;
     }
     
   if(_expiracao > 0)
      if(!MQLInfoInteger(MQL_TESTER) && !MQLInfoInteger(MQL_OPTIMIZATION))
         if(TimeCurrent() > _expiracao)
           {
            printf("Licença para uso expirada em %s. Contate o desenvolvedor",TimeToString(_expiracao,TIME_DATE));
            return false;
           }

   if(_permitidas > 0)
     {
      for(int i=ArraySize(_contas)-1; i>=0; i--)
         if(_contas[i] == conta)
           {
            printf("Esta conta foi validada com sucesso para uso");
            return true;
           }

      printf("Esta conta não está habilitada para uso. Contate o desenvolvedor");
      return false;
     }

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
string GLOBAL::set_simbolo(void)
  {
   if(m_cross_order)
      return m_cross_ativo;

   return _Symbol;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
#define M_SYMBOL in_pro.set_simbolo()
#define M_POINT  SymbolInfoDouble(M_SYMBOL,SYMBOL_POINT)
#define M_DIGITS (int)SymbolInfoInteger(M_SYMBOL,SYMBOL_DIGITS)
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::check_sinal(int &sinal, const int menu1, const double value1, const int coef1, const double var1,
                           const int sentido, const int menu2, const double value2, const int coef2, const double var2)
  {
   double valor1 = 0.0;
   double valor2 = 0.0;

   for(int i=0; i<2; i++)
     {
      double valor = 0.0;
      int menu = (i == 0) ? menu1 : menu2;
      int referencia = (i == 0) ? (int)fabs(NormalizeDouble(value1,0)) : (int)fabs(NormalizeDouble(value2,0));

      if(menu == 1)
         valor = (i == 0) ? value1 : value2;
      else
         if(menu < 10)
           {
            MqlRates rates[];
            ZeroMemory(rates);
            ArraySetAsSeries(rates,true);

            if(CopyRates(_Symbol,m_timeframe,referencia,1,rates) < 1)
              {
               filtro_log("Falha na cópia dos dados da barra");
               sinal = INT_MIN;
               return false;
              }

            if(menu < 0)
              {
               switch(fabs(menu))
                 {
                  case 1:
                     valor = rates[0].high-rates[0].low;
                     break;
                  case 2:
                     valor = fabs(rates[0].close-rates[0].open);
                     break;
                  case 3:
                     valor = EMPTY_VALUE;
                     break;
                  case 4:
                     valor = iClose(_Symbol,PERIOD_CURRENT,0);
                     break;
                 }
              }
            else
               switch(menu)
                 {
                  case 2:
                     valor = rates[0].close;
                     break;
                  case 3:
                     valor = rates[0].open;
                     break;
                  case 4:
                     valor = rates[0].high;
                     break;
                  case 5:
                     valor = rates[0].low;
                     break;
                  case 6:
                     valor = iClose(_Symbol,PERIOD_D1,referencia);
                     break;
                  case 7:
                     valor = iOpen(_Symbol,PERIOD_D1,referencia);
                     break;
                  case 8:
                     valor = iHigh(_Symbol,PERIOD_D1,referencia);
                     break;
                  case 9:
                     valor = iLow(_Symbol,PERIOD_D1,referencia);
                     break;
                 }
           }
         else
           {
            int handle = INVALID_HANDLE;
            int buffer = 0;

            if(menu < 20)
              {
               handle = _handle_1;
               buffer = menu-10;
              }
            else
               if(menu < 30)
                 {
                  handle = _handle_2;
                  buffer = menu-20;
                 }
               else
                  if(menu < 40)
                    {
                     handle = _handle_3;
                     buffer = menu-30;
                    }
                  else
                     if(menu < 50)
                       {
                        handle = _handle_4;
                        buffer = menu-40;
                       }
                     else
                        if(menu < 60)
                          {
                           handle = _handle_5;
                           buffer = menu-50;
                          }
                        else
                           if(menu < 70)
                             {
                              handle = _handle_6;
                              buffer = menu-60;
                             }
                           else
                              if(menu < 80)
                                {
                                 handle = _handle_7;
                                 buffer = menu-70;
                                }
                              else
                                 if(menu < 90)
                                   {
                                    handle = _handle_8;
                                    buffer = menu-80;
                                   }

            if(menu >= 90 || handle == INVALID_HANDLE)
              {
               filtro_log("Buffers indicador incorreto, máximo 10");
               sinal = INT_MIN;
               return false;
              }

            double price[];
            ZeroMemory(price);
            ArraySetAsSeries(price,true);

            if(CopyBuffer(handle,buffer,referencia,1,price) < 1)
              {
               filtro_log("Falha na cópia dos dados do indicador");
               sinal = INT_MIN;
               return false;
              }

            valor = price[0];
           }

      if(i == 0)
         valor1 = check_coeficiente(valor,coef1,var1);
      else
         valor2 = check_coeficiente(valor,coef2,var2);
     }

   if(check_sentido(valor1,valor2,sentido))
     {
      sinal++;
      return true;
     }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
double EXECUCAO::check_coeficiente(const double valor, const int coef, const double var)
  {
   switch(coef)
     {
      case 0:
         return (valor*var);
         break;
      case 1:
         if(var == 0.00)
            return 0.00;
         else
            return (valor/var);
         break;
      case 2:
         return (valor+var);
         break;
      case 3:
         return (valor-var);
         break;
     }

   return 0.00;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::check_sentido(const double valor1, const double valor2, const int sentido)
  {
   switch(sentido)
     {
      case 0:
         if(valor1 > valor2)
            return true;
         break;
      case 1:
         if(valor1 < valor2)
            return true;
         break;
      case 2:
         if(valor1 >= valor2)
            return true;
         break;
      case 3:
         if(valor1 <= valor2)
            return true;
         break;
      case 4:
         if(valor1 == valor2)
            return true;
         break;
      case 5:
         if(valor1 != valor2)
            return true;
         break;
      case 6:
         if(valor1 > valor2)
            return true;
         break;
      case 7:
         if(valor1 < valor2)
            return true;
         break;
      case 8:
         if(valor1 > valor2)
            return true;
         break;
      case 9:
         if(valor1 < valor2)
            return true;
         break;
     }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
double EXECUCAO::check_price(const e_price pr)
  {
   switch(pr)
     {
      case 0:
         return iClose(M_SYMBOL,m_timeframe,0);
         break;
      case 1:
         return iHigh(M_SYMBOL,m_timeframe,0);
         break;
      case 2:
         return iLow(M_SYMBOL,m_timeframe,0);
         break;
      case 3:
         return iOpen(M_SYMBOL,m_timeframe,0);
         break;
      case 4:
         return iHigh(M_SYMBOL,m_timeframe,1);
         break;
      case 5:
         return iLow(M_SYMBOL,m_timeframe,1);
         break;
      case 6:
         return iClose(M_SYMBOL,m_timeframe,1);
         break;
      case 7:
         return fmax(fmax(iHigh(M_SYMBOL,m_timeframe,0),iHigh(M_SYMBOL,m_timeframe,1)),iHigh(M_SYMBOL,m_timeframe,2));
         break;
      case 8:
         return fmin(fmin(iLow(M_SYMBOL,m_timeframe,0),iLow(M_SYMBOL,m_timeframe,1)),iLow(M_SYMBOL,m_timeframe,2));
         break;
      case 9:
         return iHigh(M_SYMBOL,PERIOD_D1,0);
         break;
      case 10:
         return iLow(M_SYMBOL,PERIOD_D1,0);
         break;
      case 11:
         return iOpen(M_SYMBOL,PERIOD_D1,0);
         break;
      case 12:
         return iHigh(M_SYMBOL,PERIOD_D1,1);
         break;
      case 13:
         return iLow(M_SYMBOL,PERIOD_D1,1);
         break;
      case 14:
         return iClose(M_SYMBOL,PERIOD_D1,1);
         break;
      default:
         return 0;
         break;
     }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void GRAFICO::filtro_log(const string msg)
  {
   static string last = NULL;

   if(msg != last)
     {
      printf("[%s][%s] %s",Expert,m_set,msg);
      last = msg;
      uint start = (m_painel) ? (_minimizado ? 75 : 393) : 25;

      if(_visual && m_log)
        {
         for(int i=ArraySize(_linhas)-1; i>0; i--)
           {
            _linhas[i] = _linhas[i-1];
            string nome = Robot+"_LOG_"+IntegerToString(i);
            ObjectSetString(0,nome,OBJPROP_TEXT,_linhas[i]);
            ObjectSetInteger(0,nome,OBJPROP_YDISTANCE,start+(15*i));
           }

         _linhas[0] = "["+TimeToString(TimeLocal(),TIME_SECONDS)+"] "+msg;
         
         if(StringLen(_linhas[0]) > 63)
            _linhas[0] = StringSubstr(_linhas[0],0,60)+"...";
            
         ObjectSetString(0,Robot+"_LOG_0",OBJPROP_TEXT,_linhas[0]);
         ObjectSetInteger(0,Robot+"_LOG_0",OBJPROP_YDISTANCE,start);
        }
     }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool GRAFICO::criar_log(void)
  {
   if(!_visual || !m_log)
      return true;

   ResetLastError();
   uint start = (m_painel) ? (_minimizado ? 75 : 393) : 25;

   for(int i=ArraySize(_linhas)-1; i>=0; i--)
     {
      string nome = Robot+"_LOG_"+IntegerToString(i);

      if(!ObjectCreate(0,nome,OBJ_LABEL,0,0,0))
        {
         _visual = false;
         string msg = StringFormat("Erro %d ao criar a linha %d do log",GetLastError(),i);
         filtro_log(msg);
         return false;
        }

      _linhas[i] = " ";
      set_obj(OBJ_LABEL,nome,10,start+(15*i),0,0,0,NULL,NULL,"Calibri",08,_linhas[i],clrGoldenrod);
     }

   ObjectSetInteger(0,Robot+"_LOG_0",OBJPROP_COLOR,clrGold);
   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void GRAFICO::set_grafico(void)
  {
   if(!_visual)
      return;

   ChartSetInteger(0,CHART_SHOW_GRID,false);
   ChartSetInteger(0,CHART_SHOW_VOLUMES,false);
   ChartSetInteger(0,CHART_EVENT_MOUSE_MOVE,false);
   ChartSetInteger(0,CHART_SHOW_LAST_LINE,true);
   ChartSetInteger(0,CHART_SHOW_BID_LINE,true);
   ChartSetInteger(0,CHART_SHOW_ASK_LINE,true);

   if(m_layout)
     {
      ChartSetInteger(0,CHART_MODE,CHART_CANDLES);
      ChartSetInteger(0,CHART_COLOR_BID,clrGray);
      ChartSetInteger(0,CHART_COLOR_ASK,clrGray);
      ChartSetInteger(0,CHART_COLOR_LAST,clrWhiteSmoke);
      ChartSetInteger(0,CHART_COLOR_CANDLE_BULL,clrBlue);
      ChartSetInteger(0,CHART_COLOR_CANDLE_BEAR,clrRed);
      ChartSetInteger(0,CHART_COLOR_CHART_UP,clrGray);
      ChartSetInteger(0,CHART_COLOR_CHART_DOWN,clrGray);
      ChartSetInteger(0,CHART_COLOR_CHART_LINE,clrGray);
      ChartSetInteger(0,CHART_COLOR_BACKGROUND,C'40,40,50');
     }

   if(m_tarjas)
     {
      ChartSetInteger(0,CHART_SHOW_TRADE_LEVELS,false);
      ChartSetInteger(0,CHART_DRAG_TRADE_LEVELS,false);
      ChartSetInteger(0,CHART_COLOR_STOP_LEVEL,clrNONE);
      ChartSetInteger(0,CHART_COLOR_VOLUME,clrNONE);
     }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool GRAFICO::minimizar_painel(void)
  {
   ResetLastError();
   if(!ObjectCreate(0,_prefix_painel+"_FUNDO_PAINEL_0",OBJ_RECTANGLE_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_FUNDO_PAINEL_1",OBJ_RECTANGLE_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_NOME_ROBO",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_MAGIC",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_SETUP",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_BOL_MINIMIZAR",OBJ_BUTTON,0,0,0))
     {
      filtro_log("Erro "+(string)GetLastError()+" ao minimizar o painel");
      return false;
     }

   string info = StringFormat("%s %s - %d",StringSubstr(EnumToString((ENUM_ACCOUNT_TRADE_MODE)AccountInfoInteger(ACCOUNT_TRADE_MODE)),19),
                              StringSubstr(EnumToString((ENUM_ACCOUNT_MARGIN_MODE)AccountInfoInteger(ACCOUNT_MARGIN_MODE)),27),m_magic);

   set_obj(OBJ_RECTANGLE_LABEL,_prefix_painel+"_FUNDO_PAINEL_0",5,20,360,52,2,clrDimGray,NULL,NULL,NULL,NULL,NULL);
   set_obj(OBJ_RECTANGLE_LABEL,_prefix_painel+"_FUNDO_PAINEL_1",6,35,358,37,0,C'50,50,50',NULL,NULL,NULL,NULL,NULL);
   set_obj(OBJ_LABEL,_prefix_painel+"_MAGIC",105,22,0,0,0,NULL,NULL,"Calibri",07,info,clrLightGray);
   set_obj(OBJ_LABEL,_prefix_painel+"_NOME_ROBO",10,37,0,0,0,NULL,NULL,"Bahnschrift Bold",11,Expert,clrGold);
   set_obj(OBJ_LABEL,_prefix_painel+"_SETUP",10,57,0,0,0,NULL,NULL,"Bahnschrift",06,m_set,clrTomato);
   set_obj(OBJ_BUTTON,_prefix_painel+"_BOL_MINIMIZAR",341,24,20,10,0,C'150,150,150',C'170,170,170',"Arial Black",07,"+",clrWhite);

   _minimizado = true;
   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool GRAFICO::criar_painel(void)
  {
   if(!_visual || !m_painel)
      return true;

   ResetLastError();
   if(!ObjectCreate(0,_prefix_painel+"_FUNDO_PAINEL_0",OBJ_RECTANGLE_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_FUNDO_PAINEL_1",OBJ_RECTANGLE_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_FUNDO_PAINEL_2",OBJ_RECTANGLE_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_FUNDO_PAINEL_3",OBJ_RECTANGLE_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_NOME_ROBO",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_OPERACIONAL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_MAGIC",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_SETUP",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_LIGA_DESLIGA",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_BOL_ON",OBJ_BUTTON,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_BOL_OFF",OBJ_BUTTON,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_BOL_BUFFERS",OBJ_BUTTON,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_POS",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_POS_VL",OBJ_EDIT,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_LOT",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_LOT_VL",OBJ_EDIT,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_LUCRO",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_LUCRO_VL",OBJ_EDIT,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_TRADE",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_TRADE_VL",OBJ_EDIT,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_DIARIO",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_DIARIO_VL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_SEMANAL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_SEMANAL_VL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_MENSAL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_MENSAL_VL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_TOTAL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_TOTAL_VL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_LAST",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_LAST_VL1",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_LAST_VL2",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_OSC",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_OSC_VL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_CANDLE",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_CANDLE_VL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_DESEMPENHO_DIA",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_DESEMPENHO_DIA_VL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_DESEMPENHO_SEM",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_DESEMPENHO_SEM_VL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_DESEMPENHO_MES",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_DESEMPENHO_MES_VL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_DESEMPENHO_TOTAL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_DESEMPENHO_TOTAL_VL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_ATUAL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_ATUAL_VL1",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_ATUAL_VL2",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_PRICE",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_PRICE_VL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_MEDIO",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_BOL_VENDER",OBJ_BUTTON,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_BOL_COMPRAR",OBJ_BUTTON,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_VOL",OBJ_EDIT,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_BOL_MAX",OBJ_BUTTON,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_BOL_MIN",OBJ_BUTTON,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_BOL_INVERTER",OBJ_BUTTON,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_BOL_ZERAR",OBJ_BUTTON,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_MEDIO_VL",OBJ_LABEL,0,0,0) ||
      !ObjectCreate(0,_prefix_painel+"_BOL_MINIMIZAR",OBJ_BUTTON,0,0,0))
     {
      filtro_log("Erro "+(string)GetLastError()+" ao criar o painel principal");
      return false;
     }

   color cor_off = (_operar) ? clrDimGray : clrDarkRed;
   color cor_on = (_operar) ? clrDarkGreen : clrDimGray;
   string msg = (_operar) ? "Expert habilitado" : "Expert desabilitado";
   string moeda = AccountInfoString(ACCOUNT_CURRENCY);
   string info = StringFormat("%s %s - %d",StringSubstr(EnumToString((ENUM_ACCOUNT_TRADE_MODE)AccountInfoInteger(ACCOUNT_TRADE_MODE)),19),
                              StringSubstr(EnumToString((ENUM_ACCOUNT_MARGIN_MODE)AccountInfoInteger(ACCOUNT_MARGIN_MODE)),27),m_magic);

   set_obj(OBJ_RECTANGLE_LABEL,_prefix_painel+"_FUNDO_PAINEL_0",5,20,360,369,2,clrDimGray,NULL,NULL,NULL,NULL,NULL);
   set_obj(OBJ_RECTANGLE_LABEL,_prefix_painel+"_FUNDO_PAINEL_1",6,35,358,53,0,C'50,50,50',NULL,NULL,NULL,NULL,NULL);
   set_obj(OBJ_RECTANGLE_LABEL,_prefix_painel+"_FUNDO_PAINEL_2",6,87,358,37,0,clrBlack,NULL,NULL,NULL,NULL,NULL);
   set_obj(OBJ_RECTANGLE_LABEL,_prefix_painel+"_FUNDO_PAINEL_3",6,169,358,68,0,clrBlack,NULL,NULL,NULL,NULL,NULL);
   set_obj(OBJ_LABEL,_prefix_painel+"_NOME_ROBO",10,37,0,0,0,NULL,NULL,"Bahnschrift Bold",11,Expert,clrGold);
   set_obj(OBJ_LABEL,_prefix_painel+"_OPERACIONAL",10,57,0,0,0,NULL,NULL,"Bahnschrift",08,msg,clrGoldenrod);
   set_obj(OBJ_LABEL,_prefix_painel+"_SETUP",10,73,0,0,0,NULL,NULL,"Bahnschrift",06,m_set,clrTomato);
   set_obj(OBJ_LABEL,_prefix_painel+"_MAGIC",105,22,0,0,0,NULL,NULL,"Calibri",07,info,clrLightGray);
   set_obj(OBJ_LABEL,_prefix_painel+"_LIGA_DESLIGA",25,95,0,0,0,NULL,NULL,"Arial Black",09,"LIGA/DESLIGA",C'230,230,230');
   set_obj(OBJ_BUTTON,_prefix_painel+"_BOL_ON",160,96,40,20,0,cor_on,clrNONE,"Arial",08,"LIG",clrWhite,_operar);
   set_obj(OBJ_BUTTON,_prefix_painel+"_BOL_OFF",210,96,40,20,0,cor_off,clrNONE,"Arial",08,"DES",clrWhite,!_operar);
   set_obj(OBJ_BUTTON,_prefix_painel+"_BOL_BUFFERS",270,96,80,20,0,clrLightSlateGray,clrNONE,"Bahnschrift",06,"LER BUFFERS",clrWhite,false);
   set_obj(OBJ_LABEL,_prefix_painel+"_POS",25,127,0,0,0,NULL,NULL,"Bahnschrift Bold",08,"STATUS",clrWhite);
   set_obj(OBJ_EDIT,_prefix_painel+"_POS_VL",80,125,90,20,0,clrSilver,NULL,"Bahnschrift Bold",08,"ZERADO",clrBlack);
   set_obj(OBJ_LABEL,_prefix_painel+"_LOT",185,127,0,0,0,NULL,NULL,"Bahnschrift Bold",08,"VOLUME",clrWhite);
   set_obj(OBJ_EDIT,_prefix_painel+"_LOT_VL",255,125,90,20,0,clrSilver,NULL,"Bahnschrift Bold",08,DoubleToString(0,_vol_digitos),clrBlack);
   set_obj(OBJ_LABEL,_prefix_painel+"_LUCRO",25,150,0,0,0,NULL,NULL,"Bahnschrift Bold",08,"LUCRO",clrWhite);
   set_obj(OBJ_EDIT,_prefix_painel+"_LUCRO_VL",80,148,90,20,0,clrSilver,NULL,"Bahnschrift Bold",08,"0.00",clrBlack);
   set_obj(OBJ_LABEL,_prefix_painel+"_TRADE",185,150,0,0,0,NULL,NULL,"Bahnschrift Bold",08,"DURAÇÃO",clrWhite);
   set_obj(OBJ_EDIT,_prefix_painel+"_TRADE_VL",255,148,90,20,0,clrSilver,NULL,"Bahnschrift Bold",08,"00:00:00",clrBlack);
   set_obj(OBJ_LABEL,_prefix_painel+"_DIARIO",10,172,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"Saldo Dia",clrWhite);
   set_obj(OBJ_LABEL,_prefix_painel+"_DIARIO_VL",100,172,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"0.00",clrDarkGray);
   set_obj(OBJ_LABEL,_prefix_painel+"_SEMANAL",10,187,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"Saldo Sem",clrWhite);
   set_obj(OBJ_LABEL,_prefix_painel+"_SEMANAL_VL",100,187,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"0.00",clrDarkGray);
   set_obj(OBJ_LABEL,_prefix_painel+"_MENSAL",10,202,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"Saldo Mês",clrWhite);
   set_obj(OBJ_LABEL,_prefix_painel+"_MENSAL_VL",100,202,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"0.00",clrDarkGray);
   set_obj(OBJ_LABEL,_prefix_painel+"_TOTAL",10,217,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"Saldo Total",clrWhite);
   set_obj(OBJ_LABEL,_prefix_painel+"_TOTAL_VL",100,217,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"0.00",clrDarkGray);
   set_obj(OBJ_LABEL,_prefix_painel+"_DESEMPENHO_DIA",185,172,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,moeda,clrWhite);
   set_obj(OBJ_LABEL,_prefix_painel+"_DESEMPENHO_DIA_VL",270,172,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"0/0 (0.0%)",clrSilver);
   set_obj(OBJ_LABEL,_prefix_painel+"_DESEMPENHO_SEM",185,187,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,moeda,clrWhite);
   set_obj(OBJ_LABEL,_prefix_painel+"_DESEMPENHO_SEM_VL",270,187,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"0/0 (0.0%)",clrSilver);
   set_obj(OBJ_LABEL,_prefix_painel+"_DESEMPENHO_MES",185,202,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,moeda,clrWhite);
   set_obj(OBJ_LABEL,_prefix_painel+"_DESEMPENHO_MES_VL",270,202,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"0/0 (0.0%)",clrSilver);
   set_obj(OBJ_LABEL,_prefix_painel+"_DESEMPENHO_TOTAL",185,217,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,moeda,clrWhite);
   set_obj(OBJ_LABEL,_prefix_painel+"_DESEMPENHO_TOTAL_VL",270,217,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"0/0 (0.0%)",clrSilver);
   set_obj(OBJ_LABEL,_prefix_painel+"_LAST",10,237,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"Hr. abertura",clrOrange);
   set_obj(OBJ_LABEL,_prefix_painel+"_LAST_VL1",100,237,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"00:00:00",clrLightGray);
   set_obj(OBJ_LABEL,_prefix_painel+"_LAST_VL2",100,252,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"0000.00.00",clrDarkGray);
   set_obj(OBJ_LABEL,_prefix_painel+"_ATUAL",185,237,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"Último trade",clrOrange);
   set_obj(OBJ_LABEL,_prefix_painel+"_ATUAL_VL1",270,237,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"00:00:00",clrLightGray);
   set_obj(OBJ_LABEL,_prefix_painel+"_ATUAL_VL2",270,252,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"0000.00.00",clrDarkGray);
   set_obj(OBJ_LABEL,_prefix_painel+"_PRICE",10,267,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"Preço entrada",clrOrange);
   set_obj(OBJ_LABEL,_prefix_painel+"_PRICE_VL",100,267,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,DoubleToString(0,M_DIGITS),clrLightGray);
   set_obj(OBJ_LABEL,_prefix_painel+"_MEDIO",185,267,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"Preço médio",clrOrange);
   set_obj(OBJ_LABEL,_prefix_painel+"_MEDIO_VL",270,267,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,DoubleToString(0,M_DIGITS),clrLightGray);
   set_obj(OBJ_LABEL,_prefix_painel+"_OSC",10,282,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"Oscilação dia",clrKhaki);
   set_obj(OBJ_LABEL,_prefix_painel+"_OSC_VL",100,282,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"0.00%",clrWhiteSmoke);
   set_obj(OBJ_LABEL,_prefix_painel+"_CANDLE",185,282,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"Nova Barra",clrKhaki);
   set_obj(OBJ_LABEL,_prefix_painel+"_CANDLE_VL",270,282,0,0,0,NULL,NULL,"Bahnschrift SemiBold",08,"--:--:--",clrWhiteSmoke);
   set_obj(OBJ_BUTTON,_prefix_painel+"_BOL_VENDER",10,302,110,45,0,C'120,40,40',clrNONE,"Arial Black",08,"VENDER",clrWhite);
   set_obj(OBJ_BUTTON,_prefix_painel+"_BOL_COMPRAR",250,302,110,45,0,C'40,40,120',clrNONE,"Arial Black",08,"COMPRAR",clrWhite);
   set_obj(OBJ_EDIT,_prefix_painel+"_VOL",145,302,100,45,0,C'200,200,200',NULL,"Arial Black",08,DoubleToString(_boleta,_vol_digitos),clrBlack);
   set_obj(OBJ_BUTTON,_prefix_painel+"_BOL_MAX",127,303,15,20,0,C'180,180,180',clrNONE,"Arial Black",08,"+",clrBlack);
   set_obj(OBJ_BUTTON,_prefix_painel+"_BOL_MIN",127,326,15,20,0,C'180,180,180',clrNONE,"Arial Black",08,"-",clrBlack);
   set_obj(OBJ_BUTTON,_prefix_painel+"_BOL_INVERTER",10,350,172,35,0,C'50,30,50',clrNONE,"Arial Black",08,"INVERTER",clrWhite);
   set_obj(OBJ_BUTTON,_prefix_painel+"_BOL_ZERAR",189,350,172,35,0,C'50,30,50',clrNONE,"Arial Black",08,"ZERAR",clrWhite);
   set_obj(OBJ_BUTTON,_prefix_painel+"_BOL_MINIMIZAR",341,24,20,10,0,C'150,150,150',C'170,170,170',"Arial Black",07,"-",clrWhite);

   _minimizado = false;
   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void GRAFICO::set_obj(const ENUM_OBJECT obj, const string nome, const int lat_dis, const int top_dis, const int larg,
                      const int alt, const int width, const color clr_fundo, const color clr_borda,
                      const string font, const int font_size, const string txt, const color clr_txt,
                      const bool press=false)
  {
   ObjectSetInteger(0,nome,OBJPROP_XDISTANCE,lat_dis);
   ObjectSetInteger(0,nome,OBJPROP_YDISTANCE,top_dis);
   ObjectSetInteger(0,nome,OBJPROP_CORNER,CORNER_LEFT_UPPER);
   ObjectSetInteger(0,nome,OBJPROP_HIDDEN,true);
   ObjectSetInteger(0,nome,OBJPROP_BACK,false);
   ObjectSetInteger(0,nome,OBJPROP_SELECTABLE,false);
   ObjectSetInteger(0,nome,OBJPROP_SELECTED,false);
   ObjectSetInteger(0,nome,OBJPROP_HIDDEN,true);
   ObjectSetInteger(0,nome,OBJPROP_ZORDER,10);
   ObjectSetInteger(0,nome,OBJPROP_ALIGN,ALIGN_CENTER);

   switch(obj)
     {
      case OBJ_RECTANGLE_LABEL:
         ObjectSetInteger(0,nome,OBJPROP_XSIZE,larg);
         ObjectSetInteger(0,nome,OBJPROP_YSIZE,alt);
         ObjectSetInteger(0,nome,OBJPROP_BGCOLOR,clr_fundo);
         ObjectSetInteger(0,nome,OBJPROP_BORDER_COLOR,clr_borda);
         ObjectSetInteger(0,nome,OBJPROP_STYLE,STYLE_SOLID);
         ObjectSetInteger(0,nome,OBJPROP_WIDTH,width);
         break;
      case OBJ_LABEL:
         ObjectSetInteger(0,nome,OBJPROP_COLOR,clr_txt);
         ObjectSetInteger(0,nome,OBJPROP_FONTSIZE,font_size);
         ObjectSetString(0,nome,OBJPROP_FONT,font);
         ObjectSetString(0,nome,OBJPROP_TEXT,txt);
         break;
      default:
         ObjectSetInteger(0,nome,OBJPROP_BGCOLOR,clr_fundo);
         ObjectSetInteger(0,nome,OBJPROP_COLOR,clr_txt);
         ObjectSetInteger(0,nome,OBJPROP_XSIZE,larg);
         ObjectSetInteger(0,nome,OBJPROP_YSIZE,alt);
         ObjectSetInteger(0,nome,OBJPROP_FONTSIZE,font_size);
         ObjectSetString(0,nome,OBJPROP_FONT,font);
         ObjectSetString(0,nome,OBJPROP_TEXT,txt);
         ObjectSetInteger(0,nome,OBJPROP_READONLY,true);
         ObjectSetInteger(0,nome,OBJPROP_BORDER_COLOR,clr_borda);
         ObjectSetInteger(0,nome,OBJPROP_STATE,press);
         break;
     }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void GRAFICO::update_painel_position(const s_position &pos)
  {
   if(!_visual || !m_painel || _minimizado)
      return;

   ObjectSetString(0,_prefix_painel+"_LOT_VL",OBJPROP_TEXT,DoubleToString(fabs(pos.volume),_vol_digitos));
   ObjectSetString(0,_prefix_painel+"_LUCRO_VL",OBJPROP_TEXT,DoubleToString(pos.lucro,2));

   if(fabs(pos.volume) > 0.00)
     {
      datetime tempo = fabs(TimeCurrent()-pos.hora);
      string dias = (tempo >= PeriodSeconds(PERIOD_D1)) ? StringFormat("%dd ",tempo/PeriodSeconds(PERIOD_D1)) : "";

      ObjectSetString(0,_prefix_painel+"_TRADE_VL",OBJPROP_TEXT,dias+TimeToString(tempo,TIME_SECONDS));
      ObjectSetString(0,_prefix_painel+"_LAST_VL1",OBJPROP_TEXT,TimeToString(pos.hora,TIME_SECONDS));
      ObjectSetString(0,_prefix_painel+"_LAST_VL2",OBJPROP_TEXT,TimeToString(pos.hora,TIME_DATE));
     }
   else
     {
      ObjectSetString(0,_prefix_painel+"_TRADE_VL",OBJPROP_TEXT,"00:00:00");
      ObjectSetString(0,_prefix_painel+"_LAST_VL1",OBJPROP_TEXT,"00:00:00");
      ObjectSetString(0,_prefix_painel+"_LAST_VL2",OBJPROP_TEXT,"0000.00.00");
     }

   if(pos.lucro == 0.00)
     {
      ObjectSetInteger(0,_prefix_painel+"_LUCRO_VL",OBJPROP_BGCOLOR,clrSilver);
      ObjectSetInteger(0,_prefix_painel+"_LUCRO_VL",OBJPROP_COLOR,clrBlack);
     }
   else
     {
      ObjectSetInteger(0,_prefix_painel+"_LUCRO_VL",OBJPROP_COLOR,clrWhite);
      if(pos.lucro > 0.0)
         ObjectSetInteger(0,_prefix_painel+"_LUCRO_VL",OBJPROP_BGCOLOR,clrGreen);
      else
         ObjectSetInteger(0,_prefix_painel+"_LUCRO_VL",OBJPROP_BGCOLOR,clrRed);
     }

   if(pos.volume == 0.00)
     {
      ObjectSetInteger(0,_prefix_painel+"_POS_VL",OBJPROP_COLOR,clrBlack);
      ObjectSetInteger(0,_prefix_painel+"_LOT_VL",OBJPROP_COLOR,clrBlack);

      ObjectSetString(0,_prefix_painel+"_POS_VL",OBJPROP_TEXT,"ZERADO");
      ObjectSetInteger(0,_prefix_painel+"_POS_VL",OBJPROP_BGCOLOR,clrSilver);
      ObjectSetInteger(0,_prefix_painel+"_LOT_VL",OBJPROP_BGCOLOR,clrSilver);
     }
   else
     {
      ObjectSetInteger(0,_prefix_painel+"_POS_VL",OBJPROP_COLOR,clrWhite);
      ObjectSetInteger(0,_prefix_painel+"_LOT_VL",OBJPROP_COLOR,clrWhite);

      if(pos.volume > 0.0)
        {
         ObjectSetString(0,_prefix_painel+"_POS_VL",OBJPROP_TEXT,"COMPRADO");
         ObjectSetInteger(0,_prefix_painel+"_POS_VL",OBJPROP_BGCOLOR,clrDarkBlue);
         ObjectSetInteger(0,_prefix_painel+"_LOT_VL",OBJPROP_BGCOLOR,clrDarkBlue);
        }
      else
        {
         ObjectSetString(0,_prefix_painel+"_POS_VL",OBJPROP_TEXT,"VENDIDO");
         ObjectSetInteger(0,_prefix_painel+"_POS_VL",OBJPROP_BGCOLOR,clrDarkOrange);
         ObjectSetInteger(0,_prefix_painel+"_LOT_VL",OBJPROP_BGCOLOR,clrDarkOrange);
        }
     }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void GRAFICO::update_painel_history(const s_history &his)
  {
   if(!_visual || !m_painel || _minimizado)
      return;

   ObjectSetString(0,_prefix_painel+"_PRICE_VL",OBJPROP_TEXT,DoubleToString(his.entrada,M_DIGITS));
   ObjectSetString(0,_prefix_painel+"_MEDIO_VL",OBJPROP_TEXT,DoubleToString(his.medio,M_DIGITS));
   ObjectSetString(0,_prefix_painel+"_DIARIO_VL",OBJPROP_TEXT,DoubleToString(his.saldo_dia,2));
   ObjectSetInteger(0,_prefix_painel+"_DIARIO_VL",OBJPROP_COLOR,confirmar_cor(his.saldo_dia));
   ObjectSetString(0,_prefix_painel+"_SEMANAL_VL",OBJPROP_TEXT,DoubleToString(his.saldo_sem,2));
   ObjectSetInteger(0,_prefix_painel+"_SEMANAL_VL",OBJPROP_COLOR,confirmar_cor(his.saldo_sem));
   ObjectSetString(0,_prefix_painel+"_MENSAL_VL",OBJPROP_TEXT,DoubleToString(his.saldo_mes,2));
   ObjectSetInteger(0,_prefix_painel+"_MENSAL_VL",OBJPROP_COLOR,confirmar_cor(his.saldo_mes));
   ObjectSetString(0,_prefix_painel+"_TOTAL_VL",OBJPROP_TEXT,DoubleToString(his.saldo_total,2));
   ObjectSetInteger(0,_prefix_painel+"_TOTAL_VL",OBJPROP_COLOR,confirmar_cor(his.saldo_total));

   if(his.ult_time > 0)
     {
      ObjectSetString(0,_prefix_painel+"_ATUAL_VL1",OBJPROP_TEXT,TimeToString((datetime)his.ult_time,TIME_SECONDS));
      ObjectSetString(0,_prefix_painel+"_ATUAL_VL2",OBJPROP_TEXT,TimeToString((datetime)his.ult_time,TIME_DATE));
     }
   else
     {
      ObjectSetString(0,_prefix_painel+"_ATUAL_VL1",OBJPROP_TEXT,"00:00:00");
      ObjectSetString(0,_prefix_painel+"_ATUAL_VL2",OBJPROP_TEXT,"0000.00.00");
     }

   double perfomace = (his.cnt_dia > 0) ? (double)(100*his.gains_dia)/his.cnt_dia : 0.0;
   string txt = StringFormat("%d/%d (%.1f%%)",his.gains_dia,his.cnt_dia,perfomace);
   ObjectSetString(0,_prefix_painel+"_DESEMPENHO_DIA_VL",OBJPROP_TEXT,txt);

   perfomace = (his.cnt_sem > 0) ? (double)(100*his.gains_sem)/his.cnt_sem : 0.0;
   txt = StringFormat("%d/%d (%.1f%%)",his.gains_sem,his.cnt_sem,perfomace);
   ObjectSetString(0,_prefix_painel+"_DESEMPENHO_SEM_VL",OBJPROP_TEXT,txt);

   perfomace = (his.cnt_mes > 0) ? (double)(100*his.gains_mes)/his.cnt_mes : 0.0;
   txt = StringFormat("%d/%d (%.1f%%)",his.gains_mes,his.cnt_mes,perfomace);
   ObjectSetString(0,_prefix_painel+"_DESEMPENHO_MES_VL",OBJPROP_TEXT,txt);

   perfomace = (his.cnt_total > 0) ? (double)(100*his.gains_total)/his.cnt_total : 0.0;
   txt = StringFormat("%d/%d (%.1f%%)",his.gains_total,his.cnt_total,perfomace);
   ObjectSetString(0,_prefix_painel+"_DESEMPENHO_TOTAL_VL",OBJPROP_TEXT,txt);
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
color GRAFICO::confirmar_cor(const double valor)
  {
   if(valor > 0.0)
      return clrGreen;
   else
      if(valor < 0.0)
         return clrRed;

   return clrDarkGray;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void GRAFICO::update_painel_descritivo(const string msg)
  {
   if(!_visual || !m_painel || _minimizado)
      return;

   ObjectSetString(0,_prefix_painel+"_OPERACIONAL",OBJPROP_TEXT,msg);
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void GRAFICO::excluir_indicadores(void)
  {
   int total = (int)ChartGetInteger(0,CHART_WINDOWS_TOTAL);

   for(int i=total-1; i>=0; i--)
      for(int k=ChartIndicatorsTotal(0,i)-1; k>=0; k--)
        {
         string short_name = ChartIndicatorName(0,i,k);
         ChartIndicatorDelete(0,i,short_name);
        }

   IndicatorRelease(_handle_1);
   IndicatorRelease(_handle_2);
   IndicatorRelease(_handle_3);
   IndicatorRelease(_handle_4);
   IndicatorRelease(_handle_5);
   IndicatorRelease(_handle_6);
   IndicatorRelease(_handle_7);
   IndicatorRelease(_handle_8);
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void GRAFICO::gerenciar_linhas(const s_position &pos, const s_ordem &ord, const ulong &grad[], const double entrada, const double medio)
  {
   if(!_atualizar || !_visual || !m_tarjas)
     {
      _atualizar = false;
      return;
     }
   else
      ObjectsDeleteAll(0,_prefix_linha,0);

   if(pos.volume == 0.00)
     {
      if(OrderSelect(ord.buy))
        {
         string txt = "Compra "+DoubleToString(OrderGetDouble(ORDER_VOLUME_CURRENT),_vol_digitos);
         criar_linha("PEN",ord.buy,txt,OrderGetDouble(ORDER_PRICE_OPEN),clrAqua,STYLE_SOLID);
        }

      if(OrderSelect(ord.sell))
        {
         string txt = "Venda "+DoubleToString(OrderGetDouble(ORDER_VOLUME_CURRENT),_vol_digitos);
         criar_linha("PEN",ord.sell,txt,OrderGetDouble(ORDER_PRICE_OPEN),clrSalmon,STYLE_SOLID);
        }
     }
   else
     {
      double mult = pos.volume*(SymbolInfoDouble(M_SYMBOL,SYMBOL_TRADE_TICK_VALUE)/SymbolInfoDouble(M_SYMBOL,SYMBOL_TRADE_TICK_SIZE));
      ulong  ordem[15] = {ord.af1,ord.af2,ord.af3,ord.af4,ord.af5,ord.ac1,ord.ac2,ord.ac3,ord.ac4,ord.ac5,ord.p1,ord.p2,ord.p3,ord.p4,ord.out};

      for(int i=ArraySize(ordem)-1; i>=0; i--)
        {
         if(!OrderSelect(ordem[i]))
            continue;

         string txt = NULL;
         color  cor = clrNONE;

         if(i <= 9)
            cor = (pos.volume > 0.00) ? clrAqua : clrSalmon;
         else
            cor = (pos.volume > 0.00) ? clrRed : clrBlue;

         if(i >= 0 && i <= 4)
            txt = "Aumento (F"+IntegerToString(i+1)+") ";
         else
            if(i >= 5 && i <= 9)
               txt = "Aumento (C"+IntegerToString(i-4)+") ";
            else
               if(i >= 10 && i <= 13)
                  txt = "Parcial ("+IntegerToString(i-9)+") ";
               else
                  txt = "Saída ";

         txt += DoubleToString(OrderGetDouble(ORDER_VOLUME_CURRENT),_vol_digitos);
         criar_linha("PEN",ordem[i],txt,OrderGetDouble(ORDER_PRICE_OPEN),cor,STYLE_DASH);
        }

      for(int i=ArraySize(grad)-1; i>=0; i--)
        {
         if(!OrderSelect(grad[i]))
            continue;

         string txt = NULL;
         color  cor = clrNONE;

         switch(i)
           {
            case 0:
               txt = "Gradiente (TP) ";
               cor = clrGreenYellow;
               break;
            default:
               txt = "Gradiente ("+IntegerToString(i)+") ";
               cor = (pos.volume > 0.00) ? clrAqua : clrSalmon;
               break;
           }

         txt += DoubleToString(OrderGetDouble(ORDER_VOLUME_CURRENT),_vol_digitos);
         criar_linha("PEN",grad[i],txt,OrderGetDouble(ORDER_PRICE_OPEN),cor,STYLE_DASH);
        }

      color  cor = (pos.volume > 0.00) ? clrSteelBlue : clrTomato;
      string txt = (pos.volume > 0.00) ? "Comprado " : "Vendido ";
      txt += DoubleToString(fabs(pos.volume),_vol_digitos);

      criar_linha("ENT",pos.ticket,"ENTRADA",entrada,clrSilver,STYLE_DASH,0,false);
      criar_linha("MED",pos.ticket,txt,medio,cor,STYLE_SOLID);
      criar_linha("PTP",pos.ticket,"TP",pos.tp,clrSeaGreen,STYLE_DASHDOT,(pos.tp-medio)*mult);
      criar_linha("PSL",pos.ticket,"SL",pos.sl,clrFireBrick,STYLE_DASHDOT,(pos.sl-medio)*mult);
     }

   _atualizar = false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool GRAFICO::criar_linha(const string nome, const ulong ticket, const string txt, const double price, const color cor,
                          const ENUM_LINE_STYLE style, const double saldo=0, const bool botao=true)
  {
   int x, y;
   ChartTimePriceToXY(0,0,0,price,x,y);
   ResetLastError();
   x = 155;
   y -= 10;

   bool alvos = (txt == "TP" || txt == "SL") ? true : false;
   int xsize = (alvos) ? 50 : 130;
   int xdist = (alvos) ? x-18 : x-20;

   string line = _prefix_linha+nome+"_"+IntegerToString(ticket);
   string fundo = line+"_FUNDO";
   string status = line+"_ETIQUETA";

   if(!ObjectCreate(0,line,OBJ_HLINE,0,0,0) ||
      !ObjectCreate(0,fundo,OBJ_RECTANGLE_LABEL,0,0,0) ||
      !ObjectCreate(0,status,OBJ_EDIT,0,0,0))
     {
      string msg = StringFormat("Erro %d ao criar a etiqueta da linha da ordem",GetLastError());
      filtro_log(msg);
      return false;
     }

   ObjectSetDouble(0,line,OBJPROP_PRICE,price);
   ObjectSetInteger(0,line,OBJPROP_COLOR,cor);
   ObjectSetInteger(0,line,OBJPROP_STYLE,style);
   ObjectSetInteger(0,line,OBJPROP_WIDTH,1);
   ObjectSetInteger(0,line,OBJPROP_BACK,true);
   ObjectSetInteger(0,line,OBJPROP_SELECTABLE,false);
   ObjectSetInteger(0,line,OBJPROP_HIDDEN,true);
   ObjectSetInteger(0,line,OBJPROP_ZORDER,1);

   set_obj(OBJ_RECTANGLE_LABEL,fundo,x,y,150,20,1,cor,cor,NULL,NULL,NULL,cor);
   ObjectSetInteger(0,fundo,OBJPROP_CORNER,CORNER_RIGHT_UPPER);

   set_obj(OBJ_EDIT,status,xdist,y+1,xsize,18,0,cor,cor,"Bahnschrift",08,txt,clrBlack);
   ObjectSetInteger(0,status,OBJPROP_CORNER,CORNER_RIGHT_UPPER);

   if(alvos)
     {
      string lucro = line+"_LUCRO";
      color cor2 = (saldo < 0.00) ? clrOrangeRed : clrMediumSpringGreen;

      if(!ObjectCreate(0,lucro,OBJ_EDIT,0,0,price))
        {
         string msg = StringFormat("Erro %d ao criar o lucro da ordem",GetLastError());
         filtro_log(msg);
         return false;
        }

      set_obj(OBJ_EDIT,lucro,xdist-xsize,y+2,80,16,0,cor2,cor2,"Bahnschrift",08,DoubleToString(saldo,2),clrBlack);
      ObjectSetInteger(0,lucro,OBJPROP_CORNER,CORNER_RIGHT_UPPER);
     }

   if(botao)
     {
      string button = line+"_BUTTON";

      if(!ObjectCreate(0,button,OBJ_BUTTON,0,0,price))
        {
         string msg = StringFormat("Erro %d ao criar o botão de controle da ordem",GetLastError());
         filtro_log(msg);
         return false;
        }

      set_obj(OBJ_BUTTON,button,x-3,y+3,16,16,0,clrBlack,clrBlack,"Arial",08,"X",clrWhite);
      ObjectSetInteger(0,button,OBJPROP_CORNER,CORNER_RIGHT_UPPER);
     }

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void GRAFICO::processar_grafico(const int id, const long lparam, const double dparam, const string sparam)
  {
   if(id == CHARTEVENT_OBJECT_CLICK)
      if(StringFind(sparam,_prefix_painel+"_BOL_") == 0)
        {
         string botao = sparam;
         StringReplace(botao,_prefix_painel+"_BOL_","_");
         processar_boleta(botao);
         return;
        }

   if(!_tarja.mover)
     {
      if(id == CHARTEVENT_OBJECT_CLICK)
         if(StringFind(sparam,_prefix_linha) == 0)
           {
            uint size = StringLen(_prefix_linha);
            bool remover = (StringFind(sparam,"_BUTTON") > 0) ? true : false;

            _tarja.etiqueta = StringSubstr(sparam,size,3);
            _tarja.ticket = StringToInteger(StringSubstr(sparam,size+4));
            StringConcatenate(_tarja.linha,_prefix_linha,_tarja.etiqueta,"_",IntegerToString(_tarja.ticket));
            _tarja.confirmado = (ObjectFind(0,_tarja.linha) == 0) ? true : false;

            if(!_tarja.confirmado)
               ZeroMemory(_tarja);
            else
               if(remover)
                  modificar_linha(_tarja.linha,_tarja.etiqueta,_tarja.ticket,true);
               else
                  if(_tarja.etiqueta != "ENT")
                     if(_tarja.etiqueta != "MED")
                        ChartSetInteger(0,CHART_EVENT_MOUSE_MOVE,true);
           }
     }
   else
      if(_tarja.confirmado)
         if(id == CHARTEVENT_CLICK)
           {
            modificar_linha(_tarja.linha,_tarja.etiqueta,_tarja.ticket,false);
            ChartSetInteger(0,CHART_EVENT_MOUSE_MOVE,false);
            ZeroMemory(_tarja);
           }

   if(_tarja.confirmado)
      if(id == CHARTEVENT_MOUSE_MOVE)
        {
         double last = ObjectGetDouble(0,_tarja.linha,OBJPROP_PRICE);
         int windown, y=(int)dparam-10;
         datetime time;
         double price;

         ChartXYToTimePrice(0,1,(int)dparam,windown,time,price);
         ObjectSetDouble(0,_tarja.linha,OBJPROP_PRICE,price);
         ObjectSetInteger(0,_tarja.linha+"_FUNDO",OBJPROP_YDISTANCE,y);
         ObjectSetInteger(0,_tarja.linha+"_ETIQUETA",OBJPROP_YDISTANCE,y+1);
         ObjectSetInteger(0,_tarja.linha+"_LUCRO",OBJPROP_YDISTANCE,y+2);
         ObjectSetInteger(0,_tarja.linha+"_BUTTON",OBJPROP_YDISTANCE,y+3);
         _tarja.mover = true;
         ChartRedraw();
        }

   if(id == CHARTEVENT_CHART_CHANGE)
     {
      double max = ChartGetDouble(0,CHART_PRICE_MAX);
      double min = ChartGetDouble(0,CHART_PRICE_MIN);
      static double last_max = 0;
      static double last_min = 0;

      if(last_max != max || last_min != min)
        {
         last_max = max;
         last_min = min;

         for(int i=ObjectsTotal(0,0,OBJ_HLINE)-1; i>=0; i--)
           {
            string name = ObjectName(0,i,0,OBJ_HLINE);

            if(StringFind(name,_prefix_linha) < 0)
               continue;

            double price = ObjectGetDouble(0,name,OBJPROP_PRICE);
            int x, y;

            ChartTimePriceToXY(0,0,0,price,x,y);
            y -= 10;

            ObjectSetInteger(0,name+"_FUNDO",OBJPROP_YDISTANCE,y);
            ObjectSetInteger(0,name+"_ETIQUETA",OBJPROP_YDISTANCE,y+1);
            ObjectSetInteger(0,name+"_LUCRO",OBJPROP_YDISTANCE,y+2);
            ObjectSetInteger(0,name+"_BUTTON",OBJPROP_YDISTANCE,y+3);
           }
        }
     }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void GRAFICO::processar_boleta(const string botao)
  {
   if(botao == "_MINIMIZAR")
     {
      ObjectsDeleteAll(0,_prefix_painel,0);

      if(_minimizado)
        {
         criar_painel();
         _atualizar = true;
         filtro_log("Painel maximizado");
        }
      else
        {
         minimizar_painel();
         filtro_log("Painel minimizado");
        }
     }
   else
      if(botao == "_ON")
        {
         ObjectSetInteger(0,_prefix_painel+"_BOL_ON",OBJPROP_BGCOLOR,clrDarkGreen);
         ObjectSetInteger(0,_prefix_painel+"_BOL_OFF",OBJPROP_BGCOLOR,clrDimGray);
         ObjectSetInteger(0,_prefix_painel+"_BOL_ON",OBJPROP_STATE,true);
         ObjectSetInteger(0,_prefix_painel+"_BOL_OFF",OBJPROP_STATE,false);
         _operar = true;
         filtro_log("Expert habilitado");
         update_painel_descritivo("Expert habilitado");
        }
      else
         if(botao == "_OFF")
           {
            ObjectSetInteger(0,_prefix_painel+"_BOL_ON",OBJPROP_BGCOLOR,clrDimGray);
            ObjectSetInteger(0,_prefix_painel+"_BOL_OFF",OBJPROP_BGCOLOR,clrDarkRed);
            ObjectSetInteger(0,_prefix_painel+"_BOL_ON",OBJPROP_STATE,false);
            ObjectSetInteger(0,_prefix_painel+"_BOL_OFF",OBJPROP_STATE,true);
            _operar = false;
            filtro_log("Expert desabilitado");
            update_painel_descritivo("Expert desabilitado");
           }
         else
           {
            string txt = StringSubstr(botao,1);
            filtro_log("Pressionado botão "+txt);

            if(botao == "_BUFFERS")
               in_pro.check_buffers();
            else
               if(botao == "_MAX" || botao == "_MIN")
                 {
                  double step = SymbolInfoDouble(M_SYMBOL,SYMBOL_VOLUME_STEP);
                  double vol = NormalizeDouble(StringToDouble(ObjectGetString(0,_prefix_painel+"_VOL",OBJPROP_TEXT)),_vol_digitos);
                  _boleta = (botao == "_MIN") ? fmax(vol-step,SymbolInfoDouble(M_SYMBOL,SYMBOL_VOLUME_MIN)) : fmin(vol+step,SymbolInfoDouble(M_SYMBOL,SYMBOL_VOLUME_MAX));
                  ObjectSetString(0,_prefix_painel+"_VOL",OBJPROP_TEXT,DoubleToString(_boleta,_vol_digitos));
                 }
               else
                  if(botao == "_INVERTER")
                    {
                     s_position pos = in_pro.posicao();

                     if(fabs(pos.volume) > 0.00)
                        if(pos.volume > 0)
                           in_pro.enviar_ordem(TRADE_ACTION_DEAL,ORDER_TYPE_SELL,SymbolInfoDouble(M_SYMBOL,SYMBOL_BID),0,0,0,fabs(pos.volume*2));
                        else
                           in_pro.enviar_ordem(TRADE_ACTION_DEAL,ORDER_TYPE_BUY,SymbolInfoDouble(M_SYMBOL,SYMBOL_ASK),0,0,0,fabs(pos.volume*2));
                    }
                  else
                     if(botao == "_ZERAR")
                        in_pro.zeragem_compulsoria();
                     else
                        if(botao == "_COMPRAR")
                           in_pro.enviar_ordem(TRADE_ACTION_DEAL,ORDER_TYPE_BUY,SymbolInfoDouble(M_SYMBOL,SYMBOL_ASK),0,0,0,_boleta);
                        else
                           if(botao == "_VENDER")
                              in_pro.enviar_ordem(TRADE_ACTION_DEAL,ORDER_TYPE_SELL,SymbolInfoDouble(M_SYMBOL,SYMBOL_BID),0,0,0,_boleta);

            ObjectSetInteger(0,_prefix_painel+"_BOL"+botao,OBJPROP_STATE,true);
            Sleep(150);
            ObjectSetInteger(0,_prefix_painel+"_BOL"+botao,OBJPROP_STATE,false);
           }

   ChartRedraw();
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool GRAFICO::modificar_linha(const string nome, const string etiqueta, const ulong ticket, const bool remover)
  {
   double linha = in_pro.normalizar(ObjectGetDouble(0,nome,OBJPROP_PRICE));

   if(etiqueta == "PEN" || etiqueta == "OTP" || etiqueta == "OSL")
     {
      if(OrderSelect(ticket))
        {
         double price = OrderGetDouble(ORDER_PRICE_OPEN);
         double sl = OrderGetDouble(ORDER_SL);
         double tp = OrderGetDouble(ORDER_TP);
         double vol = OrderGetDouble(ORDER_VOLUME_CURRENT);
         string coment = OrderGetString(ORDER_COMMENT);
         ENUM_ORDER_TYPE tipo = (ENUM_ORDER_TYPE)OrderGetInteger(ORDER_TYPE);

         if(etiqueta == "OSL")
           {
            if(remover)
               return in_pro.enviar_ordem(TRADE_ACTION_MODIFY,tipo,price,ticket,tp,0.00,vol,coment);
            else
               if(linha != sl)
                  return in_pro.enviar_ordem(TRADE_ACTION_MODIFY,tipo,price,ticket,tp,linha,vol,coment);
           }
         else
            if(etiqueta == "OTP")
              {
               if(remover)
                  return in_pro.enviar_ordem(TRADE_ACTION_MODIFY,tipo,price,ticket,0.00,sl,vol,coment);
               else
                  if(linha != tp)
                     return in_pro.enviar_ordem(TRADE_ACTION_MODIFY,tipo,price,ticket,linha,sl,vol,coment);
              }
            else
               if(remover)
                  return in_pro.enviar_ordem(TRADE_ACTION_REMOVE,tipo,price,ticket);
               else
                  if(price != linha)
                     return in_pro.enviar_ordem(TRADE_ACTION_MODIFY,tipo,linha,ticket,tp,sl,vol,coment);
        }
     }
   else
      if(PositionSelectByTicket(ticket))
        {
         double price = PositionGetDouble(POSITION_PRICE_OPEN);
         double sl = PositionGetDouble(POSITION_SL);
         double tp = PositionGetDouble(POSITION_TP);
         double vol = PositionGetDouble(POSITION_VOLUME);
         string coment = PositionGetString(POSITION_COMMENT);
         ENUM_POSITION_TYPE tipo = (ENUM_POSITION_TYPE)PositionGetInteger(POSITION_TYPE);

         if(etiqueta == "PSL")
           {
            if(remover)
               return in_pro.enviar_ordem(TRADE_ACTION_SLTP,(ENUM_ORDER_TYPE)tipo,price,ticket,tp,0.00,0,coment);
            else
               if(linha != sl)
                  return in_pro.enviar_ordem(TRADE_ACTION_SLTP,(ENUM_ORDER_TYPE)tipo,price,ticket,tp,linha,0,coment);
           }
         else
            if(etiqueta == "PTP")
              {
               if(remover)
                  return in_pro.enviar_ordem(TRADE_ACTION_SLTP,(ENUM_ORDER_TYPE)tipo,price,ticket,0.00,sl,0,coment);
               else
                  if(linha != tp)
                     return in_pro.enviar_ordem(TRADE_ACTION_SLTP,(ENUM_ORDER_TYPE)tipo,price,ticket,linha,sl,0,coment);
              }
            else
               if(etiqueta == "MED")
                  if(remover)
                    {
                     in_pro.zeragem_compulsoria();
                     return true;
                    }
        }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void HORARIO::set_horario(void)
  {
   string hora_inicio = IntegerToString(m_hr_inicio)+":"+IntegerToString(m_min_inicio);
   string hora_final = IntegerToString(m_hr_final)+":"+IntegerToString(m_min_final);
   string hora_zerar = IntegerToString(m_hr_zerar)+":"+IntegerToString(m_min_zerar);

   TimeToStruct(StringToTime(hora_inicio),_time_inicio);
   TimeToStruct(StringToTime(hora_final),_time_parar);
   TimeToStruct(StringToTime(hora_zerar),_time_zerar);
   TimeToStruct(TimeCurrent(),_time_corrente);
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool HORARIO::horario_zeragem(void)
  {
   if(m_zerar == false)
      return false;

   if(_time_corrente.hour > _time_zerar.hour || (_time_corrente.hour == _time_zerar.hour && _time_corrente.min >= _time_zerar.min))
     {
      filtro_log("Horário de zeragem compulsória");
      return true;
     }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool HORARIO::horario_operacional(void)
  {
   if(_time_inicio.hour == _time_parar.hour)
      if(_time_inicio.min == _time_parar.min)
         return true;

   if(_time_corrente.hour > _time_inicio.hour || (_time_corrente.hour == _time_inicio.hour && _time_corrente.min >= _time_inicio.min))
      if(_time_corrente.hour < _time_parar.hour || (_time_corrente.hour == _time_parar.hour && _time_corrente.min < _time_parar.min))
         return true;

   filtro_log("Fora do horário operacional");
   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool HORARIO::check_barra(const bool candle_out, const datetime time)
  {
   bool block = (candle_out) ? _block_out : _block_in;
   if(!block)
      return true;

   if(time > 0)
      if(iTime(M_SYMBOL,m_timeframe,0) <= time)
        {
         filtro_log("Vela bloqueada por execução");
         return false;
        }

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void HORARIO::atualizar_hora(void)
  {
   TimeToStruct(TimeCurrent(),_time_corrente);

   if(m_painel)
     {
      datetime proxima = iTime(_Symbol,_Period,0)+PeriodSeconds(_Period);
      datetime tempo = proxima-TimeCurrent();
      double   ontem = iClose(_Symbol,PERIOD_D1,1);
      double   osc = iClose(_Symbol,PERIOD_D1,0)/(ontem == 0 ? DBL_MIN+1 : ontem);

      ObjectSetString(0,_prefix_painel+"_OSC_VL",OBJPROP_TEXT,DoubleToString((osc*100)-100,2)+"%");
      ObjectSetString(0,_prefix_painel+"_CANDLE_VL",OBJPROP_TEXT,(tempo >= 0 ? TimeToString(tempo,TIME_SECONDS) : "--:--:--"));
     }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool HORARIO::horario_espera(void)
  {
   if(m_pausa_1_tempo > 0)
      if(m_pausa_1_dia == es_diariamente || m_pausa_1_dia == _time_corrente.day_of_week)
         if(_time_corrente.hour > m_pausa_1_hr || (_time_corrente.hour == m_pausa_1_hr && _time_corrente.min >= m_pausa_1_min))
           {
            string h = IntegerToString(m_pausa_1_hr)+":"+IntegerToString(m_pausa_1_min);
            datetime hora = StringToTime(h);

            if(!check_temporizador(hora,m_pausa_1_tempo,m_pausa_ref))
              {
               filtro_log("Horário de pausa 1 acionado");
               return true;
              }
           }

   if(m_pausa_2_tempo > 0)
      if(m_pausa_2_dia == es_diariamente || m_pausa_2_dia == _time_corrente.day_of_week)
         if(_time_corrente.hour > m_pausa_2_hr || (_time_corrente.hour == m_pausa_2_hr && _time_corrente.min >= m_pausa_2_min))
           {
            string h = IntegerToString(m_pausa_2_hr)+":"+IntegerToString(m_pausa_2_min);
            datetime hora = StringToTime(h);

            if(!check_temporizador(hora,m_pausa_2_tempo,m_pausa_ref))
              {
               filtro_log("Horário de pausa 2 acionado");
               return true;
              }
           }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
s_position CONTROLE::posicao(void)
  {
   s_position pos;
   ZeroMemory(pos);

   for(int i=PositionsTotal()-1; i>=0; i--)
     {
      ulong ticket = PositionGetTicket(i);
      PositionSelectByTicket(ticket);

      if(PositionGetString(POSITION_SYMBOL) != M_SYMBOL)
         continue;

      if(PositionGetInteger(POSITION_MAGIC) != m_magic)
         continue;

      ENUM_POSITION_TYPE tipo = (ENUM_POSITION_TYPE)PositionGetInteger(POSITION_TYPE);
      datetime hora = (datetime)PositionGetInteger(POSITION_TIME);
      double price = PositionGetDouble(POSITION_PRICE_OPEN);
      double sl = PositionGetDouble(POSITION_SL);
      double tp = PositionGetDouble(POSITION_TP);
      double volume = PositionGetDouble(POSITION_VOLUME);
      pos.lucro += PositionGetDouble(POSITION_PROFIT);

      if(tipo == POSITION_TYPE_BUY)
        {
         if(pos.volume < 0.0)
            in_pro.enviar_ordem(TRADE_ACTION_CLOSE_BY,ORDER_TYPE_SELL,0,pos.ticket,0,0,0,NULL,ticket);
         pos.volume += volume;
        }
      else
        {
         if(pos.volume > 0.0)
            in_pro.enviar_ordem(TRADE_ACTION_CLOSE_BY,ORDER_TYPE_BUY,0,pos.ticket,0,0,0,NULL,ticket);
         pos.volume -= volume;
        }

      if(hora < pos.hora || pos.hora == 0)
        {
         pos.ticket = ticket;
         pos.sl = sl;
         pos.tp = tp;
         pos.hora = hora;
        }
      else
         if(sl != pos.sl || tp != pos.tp)
            in_pro.enviar_ordem(TRADE_ACTION_SLTP,(ENUM_ORDER_TYPE)tipo,price,ticket,pos.tp,pos.sl,volume,PositionGetString(POSITION_COMMENT));
     }

   update_painel_position(pos);
   return pos;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
s_ordem CONTROLE::ordens(ulong &grad_ticket[], const datetime abertura, const double pos_tp=0.00, const double pos_sl=0.00)
  {
   s_ordem ord;
   ZeroMemory(ord);
   ZeroMemory(grad_ticket);

   for(int i=OrdersTotal()-1; i>=0; i--)
     {
      ulong ticket = OrderGetTicket(i);
      if(OrderSelect(ticket) == false)
         continue;

      if(OrderGetInteger(ORDER_MAGIC) != m_magic)
         continue;

      if(OrderGetString(ORDER_SYMBOL) != M_SYMBOL)
         continue;

      string comentario = OrderGetString(ORDER_COMMENT);
      string coment = StringSubstr(comentario,0,4);
      double price = OrderGetDouble(ORDER_PRICE_OPEN);
      ENUM_ORDER_TYPE tipo = (ENUM_ORDER_TYPE)OrderGetInteger(ORDER_TYPE);
      ENUM_ORDER_STATE state = (ENUM_ORDER_STATE)OrderGetInteger(ORDER_STATE);
      datetime hora = (datetime)OrderGetInteger(ORDER_TIME_SETUP);
      bool repetida = false;

      if(coment == "GIN#")
        {
         int id = (int)StringSubstr(comentario,4,StringFind(comentario,"#",4)-4);

         if(id > m_grad_qtd || id < 0)
            filtro_log("Divergência nas ordens do gradiente");
         else
            if(grad_ticket[id] == 0)
               grad_ticket[id] = ticket;
            else
               repetida = true;
        }
      else
        {
         string nome[18] = {"AF1#","AF2#","AF3#","AF4#","AF5#","AC1#","AC2#","AC3#","AC4#","AC5#","SP1#","SP2#","SP3#","SP4#","CIN#","VIN#","OUT#","GTP#"};
         ulong  ordem[18] = {ord.af1,ord.af2,ord.af3,ord.af4,ord.af5,ord.ac1,ord.ac2,ord.ac3,ord.ac4,
                             ord.ac5,ord.p1,ord.p2,ord.p3,ord.p4,ord.buy,ord.sell,ord.out,grad_ticket[0]
                            };

         for(int k=0; k<18; k++)
            if(coment == nome[k])
               if(ordem[k] > 0)
                  repetida = true;
               else
                 {
                  switch(k)
                    {
                     case 0:
                        ord.af1 = ticket;
                        break;
                     case 1:
                        ord.af2 = ticket;
                        break;
                     case 2:
                        ord.af3 = ticket;
                        break;
                     case 3:
                        ord.af4 = ticket;
                        break;
                     case 4:
                        ord.af5 = ticket;
                        break;
                     case 5:
                        ord.ac1 = ticket;
                        break;
                     case 6:
                        ord.ac2 = ticket;
                        break;
                     case 7:
                        ord.ac3 = ticket;
                        break;
                     case 8:
                        ord.ac4 = ticket;
                        break;
                     case 9:
                        ord.ac5 = ticket;
                        break;
                     case 10:
                        ord.p1 = ticket;
                        break;
                     case 11:
                        ord.p2 = ticket;
                        break;
                     case 12:
                        ord.p3 = ticket;
                        break;
                     case 13:
                        ord.p4 = ticket;
                        break;
                     case 14:
                        ord.buy = ticket;
                        break;
                     case 15:
                        ord.sell = ticket;
                        break;
                     case 16:
                        ord.out = ticket;
                        if(m_cancel_out > 0)
                           if(hora+m_cancel_out <= TimeCurrent())
                              repetida = true;
                        break;
                     case 17:
                        grad_ticket[0] = ticket;
                        break;
                    }
                  break;
                 }
        }

      if(coment == "VIN#" || coment == "CIN#")
        {
         if(!in_pro.horario_operacional())
            repetida = true;

         if(!repetida)
            if(in_pro.horario_zeragem())
               repetida = true;
            else
               if(m_cancel_in > 0)
                  if(hora+m_cancel_in <= TimeCurrent())
                     repetida = true;
        }
      else
         if(coment != "SP1#" && coment != "SP2#" && coment != "SP3#" && coment != "SP4#" && coment != "OUT#" && coment != "GIN#" && coment != "GTP#")
           {
            double tp = OrderGetDouble(ORDER_TP);
            double sl = OrderGetDouble(ORDER_SL);

            if(tipo ==  ORDER_TYPE_BUY_STOP || tipo ==  ORDER_TYPE_BUY_LIMIT)
              {
               if((price >= pos_tp && pos_tp > 0.00) || price <= pos_sl)
                  repetida = true;
              }
            else
               if(price <= pos_tp || (price >= pos_sl && pos_sl > 0.00))
                  repetida = true;

            if(!repetida)
               if(sl != pos_sl || tp != pos_tp)
                  in_pro.enviar_ordem(TRADE_ACTION_MODIFY,tipo,price,ticket,pos_tp,pos_sl,OrderGetDouble(ORDER_VOLUME_CURRENT),comentario);
           }

      if(repetida || (coment != "VIN#" && coment != "CIN#" && (hora < abertura || abertura == 0)))
         if(state != ORDER_STATE_PARTIAL || repetida)
            in_pro.enviar_ordem(TRADE_ACTION_REMOVE,tipo,price,ticket);
     }

   return ord;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
s_history CONTROLE::historico(int &grad_qtd[], const datetime abertura=0)
  {
   static s_history his = {0};
   static datetime ult_data = 0;
   static int last_total = 0;

   datetime hora_atual = TimeCurrent();
   datetime dia = StringToTime(TimeToString(hora_atual,TIME_DATE));
   datetime sem = iTime(M_SYMBOL,PERIOD_W1,0);
   datetime mes = iTime(M_SYMBOL,PERIOD_MN1,0);

   datetime start = (m_total) ? 0 : fmin(sem,mes);
   HistorySelect(start,hora_atual+2);
   int total = HistoryDealsTotal();

   if(total != last_total)
      _atualizar = true;

   if(dia > ult_data || _atualizar)
     {
      ZeroMemory(his);
      ZeroMemory(grad_qtd);
     }
   else
      return his;

   double vol = 0.00;
   int opostas_dia = 0;
   int opostas_sem = 0;
   int opostas_mes = 0;
   int opostas_total = 0;
   ulong grad[];

   for(int i=0; i<total; i++)
     {
      ulong ticket = HistoryDealGetTicket(i);
      if(ticket <= 0)
         continue;

      if(HistoryDealGetInteger(ticket,DEAL_MAGIC) != m_magic)
         continue;

      if(HistoryDealGetString(ticket,DEAL_SYMBOL) != M_SYMBOL)
         continue;

      ENUM_DEAL_TYPE tipo = (ENUM_DEAL_TYPE)HistoryDealGetInteger(ticket,DEAL_TYPE);

      if(tipo != DEAL_TYPE_BUY && tipo != DEAL_TYPE_SELL)
         continue;

      datetime hora = (datetime)HistoryDealGetInteger(ticket,DEAL_TIME);
      double   price = HistoryDealGetDouble(ticket,DEAL_PRICE);
      double   lucro = HistoryDealGetDouble(ticket,DEAL_PROFIT);
      double   volume = HistoryDealGetDouble(ticket,DEAL_VOLUME);
      ENUM_DEAL_ENTRY entry = (ENUM_DEAL_ENTRY)HistoryDealGetInteger(ticket,DEAL_ENTRY);

      his.saldo_total += lucro;
      bool saida = (entry == DEAL_ENTRY_OUT || entry == DEAL_ENTRY_OUT_BY) ? true : false;

      if(saida)
        {
         his.cnt_total++;
         if(lucro > 0.00)
            his.gains_total++;

         if(entry == DEAL_ENTRY_OUT_BY)
            opostas_total++;
        }

      if(m_refere == es_dia)
         his.saldo = his.saldo_dia;

      if(hora >= dia)
        {
         his.saldo_dia += lucro;

         if(saida)
           {
            his.cnt_dia++;
            if(lucro > 0.00)
               his.gains_dia++;
           }

         if(m_refere == es_dia)
            his.saldo = his.saldo_dia;

         if(entry == DEAL_ENTRY_OUT_BY)
            opostas_dia++;
        }

      if(hora >= sem)
        {
         his.saldo_sem += lucro;

         if(saida)
           {
            his.cnt_sem++;
            if(lucro > 0.00)
               his.gains_sem++;
           }

         if(m_refere == es_sem)
            his.saldo = his.saldo_sem;

         if(entry == DEAL_ENTRY_OUT_BY)
            opostas_sem++;
        }

      if(hora >= mes)
        {
         his.saldo_mes += lucro;

         if(saida)
           {
            his.cnt_mes++;
            if(lucro > 0.00)
               his.gains_mes++;
           }

         if(m_refere == es_mes)
            his.saldo = his.saldo_mes;

         if(entry == DEAL_ENTRY_OUT_BY)
            opostas_mes++;
        }

      if(his.saldo > his.max)
         his.max = his.saldo;

      if(his.saldo < his.min)
         his.min = his.saldo;

      if(hora >= his.ult_time)
         his.ult_time = hora;

      if(abertura > 0)
         if(hora >= abertura)
           {
            if(hora == abertura)
               if(his.entrada == 0)
                  his.entrada = price;

            string comentario = HistoryDealGetString(ticket,DEAL_COMMENT);
            string coment = StringSubstr(comentario,0,4);

            if(coment == "GIN#" || coment == "GTP#")
              {
               int pos = ArraySize(grad);

               if(coment == "GTP#")
                 {
                  grad_qtd[0]++;
                  if(pos > 0)
                    {
                     ArrayRemove(grad,pos,1);
                     ArrayResize(grad,pos-1,1);
                    }
                 }
               else
                 {
                  int id = (int)StringSubstr(comentario,4,StringFind(comentario,"#",4)-4);

                  if(id > m_grad_qtd || id < 0)
                     filtro_log("Divergência no histórico do gradiente");
                  else
                    {
                     ArrayResize(grad,pos+1,1);
                     grad[pos] = ticket;
                     grad_qtd[id]++;
                    }
                 }
              }
            else
               if(coment == "AF1#")
                  his.af1 = ticket;
               else
                  if(coment == "AF2#")
                     his.af2 = ticket;
                  else
                     if(coment == "AF3#")
                        his.af3 = ticket;
                     else
                        if(coment == "AF4#")
                           his.af4 = ticket;
                        else
                           if(coment == "AF5#")
                              his.af5 = ticket;
                           else
                              if(coment == "AC1#")
                                 his.ac1 = ticket;
                              else
                                 if(coment == "AC2#")
                                    his.ac2 = ticket;
                                 else
                                    if(coment == "AC3#")
                                       his.ac3 = ticket;
                                    else
                                       if(coment == "AC4#")
                                          his.ac4 = ticket;
                                       else
                                          if(coment == "AC5#")
                                             his.ac5 = ticket;
                                          else
                                             if(coment == "SP1#")
                                                his.p1 = ticket;
                                             else
                                                if(coment == "SP2#")
                                                   his.p2 = ticket;
                                                else
                                                   if(coment == "SP3#")
                                                      his.p3 = ticket;
                                                   else
                                                      if(coment == "SP4#")
                                                         his.p4 = ticket;

            if(_ajustar || (coment != "SP1#" && coment != "SP2#" && coment != "SP3#" && coment != "SP4#" && coment != "GTP#"))
               if(entry != DEAL_ENTRY_OUT_BY)
                  if(tipo == DEAL_TYPE_BUY)
                    {
                     vol += volume;
                     his.medio += (price*volume);
                    }
                  else
                    {
                     vol -= volume;
                     his.medio -= (price*volume);
                    }
           }
     }

   his.cnt_dia -= (opostas_dia/2);
   his.cnt_sem -= (opostas_sem/2);
   his.cnt_mes -= (opostas_mes/2);
   his.cnt_total -= (opostas_total/2);

   if(!m_total)
     {
      his.cnt_total = 0;
      his.gains_total = 0;
      his.saldo_total = 0;
     }

   his.medio = (vol == 0.00) ? 0.00 : fabs(his.medio/vol);

   if(his.entrada > 0.00 && his.medio <= 0.00)
      his.medio = his.entrada;

   update_painel_history(his);
   ult_data = dia;
   last_total = total;

   if(m_grad_qtd > 0)
     {
      int pos = ArraySize(grad);

      if(pos > 0)
         if(grad[pos-1] > 0)
            his.last = grad[pos-1];
     }

   return his;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool CONTROLE::check_volumes(void)
  {
   if(!check_volume_inicial(m_volume))
      return false;

   if(m_af1_dis > 0 && m_af1_lot > 0)
      if(!check_volume_inicial(m_af1_lot))
         return false;

   if(m_af2_dis > 0 && m_af2_lot > 0)
      if(!check_volume_inicial(m_af2_lot))
         return false;

   if(m_af3_dis > 0 && m_af3_lot > 0)
      if(!check_volume_inicial(m_af3_lot))
         return false;

   if(m_af4_dis > 0 && m_af4_lot > 0)
      if(!check_volume_inicial(m_af4_lot))
         return false;

   if(m_af5_dis > 0 && m_af5_lot > 0)
      if(!check_volume_inicial(m_af5_lot))
         return false;

   if(m_ac1_dis > 0 && m_ac1_lot > 0)
      if(!check_volume_inicial(m_ac1_lot))
         return false;

   if(m_ac2_dis > 0 && m_ac2_lot > 0)
      if(!check_volume_inicial(m_ac2_lot))
         return false;

   if(m_ac3_dis > 0 && m_ac3_lot > 0)
      if(!check_volume_inicial(m_ac3_lot))
         return false;

   if(m_ac4_dis > 0 && m_ac4_lot > 0)
      if(!check_volume_inicial(m_ac4_lot))
         return false;

   if(m_ac5_dis > 0 && m_ac5_lot > 0)
      if(!check_volume_inicial(m_ac5_lot))
         return false;

   if(fabs(m_p1_dis) > 0 && m_p1_lot > 0)
      if(!check_volume_inicial(m_p1_lot))
         return false;

   if(fabs(m_p2_dis) > 0 && m_p2_lot > 0)
      if(!check_volume_inicial(m_p2_lot))
         return false;

   if(fabs(m_p3_dis) > 0 && m_p3_lot > 0)
      if(!check_volume_inicial(m_p3_lot))
         return false;

   if(fabs(m_p4_dis) > 0 && m_p4_lot > 0)
      if(!check_volume_inicial(m_p4_lot))
         return false;

   if(m_grad_qtd > 0 && m_gra_dis > 0)
      if(!check_volume_inicial(m_grad_vol))
         return false;

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool CONTROLE::check_volume_inicial(const double volume)
  {
   double max = SymbolInfoDouble(M_SYMBOL,SYMBOL_VOLUME_MAX);
   double min = SymbolInfoDouble(M_SYMBOL,SYMBOL_VOLUME_MIN);
   double step = SymbolInfoDouble(M_SYMBOL,SYMBOL_VOLUME_STEP);
   double resto = NormalizeDouble(MathMod(volume*100000,step*100000),0);

   if(_vol_digitos < 0)
     {
      for(int i=0; i<5; i++)
         if(pow(10,i)*min >= 1.00)
           {
            _vol_digitos = i;
            break;
           }

      for(int i=fmax(_vol_digitos,0); i<5; i++)
         if(pow(10,i)*step >= 1.00)
           {
            _vol_digitos = i;
            break;
           }
     }

   if(volume < min || volume > max)
     {
      string msg = "Volume de "+DoubleToString(volume,_vol_digitos)+" fora da faixa de "+DoubleToString(min,_vol_digitos)+" a "+DoubleToString(max,_vol_digitos);
      filtro_log(msg);
      return false;
     }

   if(resto > 0.0)
     {
      string msg = "Volume de "+DoubleToString(volume,_vol_digitos)+" fora do passo de "+DoubleToString(step,_vol_digitos);
      filtro_log(msg);
      return false;
     }

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void CONTROLE::check_windows(const int &window[])
  {
   if(m_inserir && _visual)
      for(int i=0; i<8; i++)
         if(window[i] >= 0)
           {
            int total = (int)ChartGetInteger(0,CHART_WINDOWS_TOTAL);
            int handle = INVALID_HANDLE;

            switch(i)
              {
               case 0:
                  handle = _handle_1;
                  break;
               case 1:
                  handle = _handle_2;
                  break;
               case 2:
                  handle = _handle_3;
                  break;
               case 3:
                  handle = _handle_4;
                  break;
               case 4:
                  handle = _handle_5;
                  break;
               case 5:
                  handle = _handle_6;
                  break;
               case 6:
                  handle = _handle_7;
                  break;
               case 7:
                  handle = _handle_8;
                  break;
              }

            if(handle != INVALID_HANDLE)
               if(window[i] == 0)
                  ChartIndicatorAdd(0,0,handle);
               else
                  if(ChartIndicatorAdd(0,total,handle))
                     total++;
           }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool CONTROLE::check_ativo(void)
  {
   if(!m_cross_order)
      return true;

   bool personalizado;

   if(!SymbolExist(m_cross_ativo,personalizado))
     {
      filtro_log("Falha no cross order. O ativo ("+m_cross_ativo+") não existe");
      return false;
     }
   else
      if(SymbolSelect(m_cross_ativo,true))
         filtro_log("Ativo ("+m_cross_ativo+") validado com sucesso para cross order");
      else
        {
         filtro_log("Falha ao selecionar o ativo cross-order no observador de mercado");
         return false;
        }

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool CONTROLE::check_ticks(void)
  {
   MqlTick tick;
   ZeroMemory(tick);

   if(!SymbolInfoTick(M_SYMBOL,tick))
     {
      string msg = StringFormat("Falha na atualização dos ticks em %s",M_SYMBOL);
      update_painel_descritivo(msg);
      filtro_log(msg);
      return false;
     }

   if(tick.ask <= 0.0 || tick.bid <= 0.0)
     {
      string msg = StringFormat("Falha na coleta da cotação em %s",M_SYMBOL);
      update_painel_descritivo(msg);
      filtro_log(msg);
      return false;
     }

   if(tick.bid > tick.ask)
     {
      string msg = StringFormat("Ativo %s em leilão",M_SYMBOL);
      update_painel_descritivo(msg);
      filtro_log(msg);
      return false;
     }

   if(tick.time+60 <= TimeCurrent())
     {
      string msg = StringFormat("Um minuto sem novos ticks em %s",M_SYMBOL);
      update_painel_descritivo(msg);
      filtro_log(msg);
      return false;
     }

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool CONTROLE::check_filling(const ENUM_TRADE_REQUEST_ACTIONS action, ENUM_ORDER_TYPE_FILLING &filling)
  {
   if(_validade == ORDER_TIME_GTC)
     {
      int flag = (int)SymbolInfoInteger(M_SYMBOL,SYMBOL_EXPIRATION_MODE);

      if((flag&SYMBOL_EXPIRATION_GTC) == 0)
         _validade = ORDER_TIME_DAY;
     }

   ENUM_SYMBOL_TRADE_EXECUTION exec = (ENUM_SYMBOL_TRADE_EXECUTION)SymbolInfoInteger(M_SYMBOL,SYMBOL_TRADE_EXEMODE);
   uint modo = (uint)SymbolInfoInteger(M_SYMBOL,SYMBOL_FILLING_MODE);

   if(exec == SYMBOL_TRADE_EXECUTION_REQUEST || exec == SYMBOL_TRADE_EXECUTION_INSTANT)
      return true;

   if(action == TRADE_ACTION_PENDING)
     {
      if(exec == SYMBOL_TRADE_EXECUTION_MARKET)
         return true;

      filling = ORDER_FILLING_RETURN;
      return true;
     }
   else
     {
      if(_filling == ORDER_FILLING_RETURN)
        {
         filling = ORDER_FILLING_RETURN;
         return true;
        }

      if((modo&SYMBOL_FILLING_FOK) == SYMBOL_FILLING_FOK)
        {
         filling = ORDER_FILLING_FOK;
         return true;
        }

      if((modo&SYMBOL_FILLING_IOC) == SYMBOL_FILLING_IOC)
        {
         filling = ORDER_FILLING_IOC;
         return true;
        }
     }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool CONTROLE::check_expiration(ENUM_ORDER_TYPE_TIME &type_time)
  {
   int flags = (int)SymbolInfoInteger(M_SYMBOL,SYMBOL_EXPIRATION_MODE);
   type_time = _validade;

   switch(_validade)
     {
      case ORDER_TIME_GTC:
         if((flags&SYMBOL_EXPIRATION_GTC) != 0)
            return true;
         else
            if((flags&SYMBOL_EXPIRATION_DAY) != 0)
              {
               type_time = ORDER_TIME_DAY;
               return true;
              }
         break;
      case ORDER_TIME_DAY:
         if((flags&SYMBOL_EXPIRATION_DAY) != 0)
            return true;
         else
            if((flags&SYMBOL_EXPIRATION_GTC) != 0)
              {
               type_time = ORDER_TIME_GTC;
               return true;
              }
         break;
      default:
         filtro_log("Tipo de expiração inválida");
     }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool CONTROLE::check_metas(const double saldo, const double lucro, const double max, const double min)
  {
   if(m_refere == es_off)
      return false;

   double gain = (m_gain_out) ? (saldo+lucro) : saldo;
   double loss = (m_loss_out) ? (saldo+lucro) : saldo;
   double dd = (m_dd_out) ? (saldo+lucro) : saldo;
   double rec = (m_rec_out) ? (saldo+lucro) : saldo;

   if(fabs(m_gain) > 0)
      if(NormalizeDouble(gain,2) >= fabs(m_gain))
        {
         string msg = StringFormat("Meta de ganho de %.2f batida",m_gain);
         filtro_log(msg);
         update_painel_descritivo(msg);
         return true;
        }

   if(fabs(m_loss) > 0)
      if(NormalizeDouble(loss,2) <= -fabs(m_loss))
        {
         string msg = StringFormat("Limite de loss %.2f acionado",m_loss);
         filtro_log(msg);
         update_painel_descritivo(msg);
         return true;
        }

   if(fabs(m_dd) > 0)
      if(max >= fabs(m_dd_gat))
         if(max-dd >= fabs(m_dd))
           {
            string msg = StringFormat("Rebaixamento máximo de %.2f acionado",m_dd);
            filtro_log(msg);
            update_painel_descritivo(msg);
            return true;
           }

   if(fabs(m_rec) > 0)
      if(min <= -fabs(m_rec_gat))
         if(rec-min >= fabs(m_rec))
           {
            string msg = StringFormat("Recuperação de %.2f acionada",m_rec);
            filtro_log(msg);
            update_painel_descritivo(msg);
            return true;
           }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool CONTROLE::check_conexao(void)
  {
   if(!TerminalInfoInteger(TERMINAL_TRADE_ALLOWED))
     {
      update_painel_descritivo("Trade desabilitado no terminal");
      return false;
     }

   if(!TerminalInfoInteger(TERMINAL_CONNECTED))
     {
      filtro_log("Sem conexão com o servidor");
      update_painel_descritivo("Sem conexão com o servidor");
      return false;
     }

   if(!AccountInfoInteger(ACCOUNT_TRADE_ALLOWED))
     {
      filtro_log("Conta desabilitada para algo trading");
      update_painel_descritivo("Conta desabilitada para algo trading");
      return false;
     }

   if(!AccountInfoInteger(ACCOUNT_TRADE_EXPERT))
     {
      filtro_log("Não permitido robô nesta conta");
      update_painel_descritivo("Não permitido robô nesta conta");
      return false;
     }

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void CONTROLE::check_visual(void)
  {
   _visual = true;

   if(MQLInfoInteger(MQL_OPTIMIZATION))
      _visual = false;
   else
      if(MQLInfoInteger(MQL_TESTER))
        {
         _teste = true;
         _visual = MQLInfoInteger(MQL_VISUAL_MODE);
        }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool CONTROLE::check_espera(const datetime time, const int espera)
  {
   if(espera <= 0)
      return true;

   if(check_temporizador(time,espera,m_espera_ref))
      return true;

   filtro_log("Sinais bloqueados pelo temporizador");
   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool CONTROLE::check_temporizador(const datetime time, const int espera, const e_tempo referencia)
  {
   switch(referencia)
     {
      case 0:
         if(TimeCurrent() >= time+espera)
            return true;
         break;
      case 1:
         if(TimeCurrent() >= time+(espera*PeriodSeconds(PERIOD_M1)))
            return true;
         break;
      case 2:
         if(TimeCurrent() >= time+(espera*PeriodSeconds(PERIOD_H1)))
            return true;
         break;
      case 3:
         if(iTime(M_SYMBOL,m_timeframe,espera-1) > time)
            return true;
         break;
     }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void CONTROLE::iniciar_handles(void)
  {
   _handle_1 = INVALID_HANDLE;
   _handle_2 = INVALID_HANDLE;
   _handle_3 = INVALID_HANDLE;
   _handle_4 = INVALID_HANDLE;
   _handle_5 = INVALID_HANDLE;
   _handle_6 = INVALID_HANDLE;
   _handle_7 = INVALID_HANDLE;
   _handle_8 = INVALID_HANDLE;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void CONTROLE::check_buffers(void)
  {
   double buffers[];
   ArraySetAsSeries(buffers,true);

   for(int k=1; k<=8; k++)
     {
      int cnt = 0;
      int handle = INVALID_HANDLE;
      string nome;

      switch(k)
        {
         case 1:
            handle = _handle_1;
            nome = "Indicador [1]";
            break;
         case 2:
            handle = _handle_2;
            nome = "Indicador [2]";
            break;
         case 3:
            handle = _handle_3;
            nome = "Indicador [3]";
            break;
         case 4:
            handle = _handle_4;
            nome = "Indicador [4]";
            break;
         case 5:
            handle = _handle_5;
            nome = "[Indicador Canais]";
            break;
         case 6:
            handle = _handle_6;
            nome = "[Sinal Rápido]";
            break;
         case 7:
            handle = _handle_7;
            nome = "[Sinal Lento]";
            break;
         case 8:
            handle = _handle_8;
            nome = "[Oscilador]";
            break;
        }

      if(handle != INVALID_HANDLE)
         for(int i=0; i<255; i++)
           {
            ZeroMemory(buffers);

            if(CopyBuffer(handle,i,0,2,buffers) == 2)
              {
               string n1 = (buffers[0] == EMPTY_VALUE) ? "EMPTY VALUE" : ((buffers[0] == DBL_MIN) ? "DBL MIN" : DoubleToString(buffers[0]));
               string n2 = (buffers[1] == EMPTY_VALUE) ? "EMPTY VALUE" : ((buffers[1] == DBL_MIN) ? "DBL MIN" : DoubleToString(buffers[1]));

               filtro_log(nome+" -> Buffer "+(string)i+" |Atual:"+n1+"| Anterior:"+n2);
               cnt++;
              }

            if(i == 254)
               if(cnt == 0)
                  filtro_log(nome+" -> ERRO: NENHUM BUFFER RECONHECIDO");
               else
                  filtro_log(nome+" -> Total de buffers: "+(string)cnt);
           }
     }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::check_permissao(void)
  {
   for(int i=OrdersTotal()-1; i>=0; i--)
     {
      ulong ticket = OrderGetTicket(i);
      if(OrderSelect(ticket) == false)
         continue;

      if(OrderGetString(ORDER_SYMBOL) != M_SYMBOL)
         continue;

      ENUM_ORDER_TYPE tipo = (ENUM_ORDER_TYPE)OrderGetInteger(ORDER_TYPE);

      if(tipo == ORDER_TYPE_BUY || tipo == ORDER_TYPE_SELL)
        {
         string msg = StringFormat("Operação negada. Aguardando ordem #%d",ticket);
         filtro_log(msg);
         return false;
        }
     }

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::check_stoplevel(double &price, const ENUM_ORDER_TYPE tipo, const bool corrigir=false, const double ajustar=0.00)
  {
   double stoplevel = SymbolInfoInteger(M_SYMBOL,SYMBOL_TRADE_STOPS_LEVEL)*M_POINT;
   double bid = (ajustar > 0) ? ajustar : SymbolInfoDouble(M_SYMBOL,SYMBOL_BID);
   double ask = (ajustar > 0) ? ajustar : SymbolInfoDouble(M_SYMBOL,SYMBOL_ASK);

   switch(tipo)
     {
      case ORDER_TYPE_BUY_LIMIT:
         if(price > ask-stoplevel)
            if(corrigir)
               price = normalizar(ask-stoplevel);
            else
              {
               string msg;
               StringConcatenate(msg,"Compra limit (",DoubleToString(price,M_DIGITS),") negado por stoplevel de ",DoubleToString(ask-stoplevel,M_DIGITS));
               filtro_log(msg);
               return false;
              }
         break;
      case ORDER_TYPE_SELL_LIMIT:
         if(price < bid+stoplevel)
            if(corrigir)
               price = normalizar(bid+stoplevel);
            else
              {
               string msg;
               StringConcatenate(msg,"Venda limit (",DoubleToString(price,M_DIGITS),") negado por stoplevel de ",DoubleToString(bid+stoplevel,M_DIGITS));
               filtro_log(msg);
               return false;
              }
         break;
      case ORDER_TYPE_BUY_STOP:
         if(price < ask+stoplevel)
            if(corrigir)
               price = normalizar(ask+stoplevel);
            else
              {
               string msg;
               StringConcatenate(msg,"Compra gatilho (",DoubleToString(price,M_DIGITS),") negado por stoplevel de ",DoubleToString(ask+stoplevel,M_DIGITS));
               filtro_log(msg);
               return false;
              }
         break;
      case ORDER_TYPE_SELL_STOP:
         if(price > bid-stoplevel)
            if(corrigir)
               price = normalizar(bid-stoplevel);
            else
              {
               string msg;
               StringConcatenate(msg,"Venda gatilho (",DoubleToString(price,M_DIGITS),") negado por stoplevel de ",DoubleToString(bid-stoplevel,M_DIGITS));
               filtro_log(msg);
               return false;
              }
         break;
     }

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::check_spread()
  {
   if(m_spread <= 0.0)
      return true;

   long spr = SymbolInfoInteger(M_SYMBOL,SYMBOL_SPREAD);

   if(spr > m_spread)
     {
      string msg = StringFormat("Ordem negada. Spread %d excede limite de %d",spr,m_spread);
      filtro_log(msg);
      update_painel_descritivo("Fora de spread");
      return false;
     }

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
double EXECUCAO::check_conversao(const bool pts, const double valor, const double price=0.0)
  {
   double resul = (pts) ? valor*M_POINT : price*valor*0.01;
   return NormalizeDouble(resul,M_DIGITS);
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::enviar_compra(void)
  {
   if(!_comprar)
      return false;

   if(!check_permissao())
      return false;

   if(!check_spread())
      return false;

   double ask = SymbolInfoDouble(M_SYMBOL,SYMBOL_ASK);
   double price = (m_price_buy == 0 || !m_pendente_in) ? ask : check_price(m_price_buy);

   if(fabs(m_dis_in) > 0 && m_pendente_in)
      price = normalizar(price+check_conversao(_pts_inout,m_dis_in,price));

   ENUM_TRADE_REQUEST_ACTIONS action = TRADE_ACTION_DEAL;
   ENUM_ORDER_TYPE tipo = ORDER_TYPE_BUY;

   if(m_pendente_in)
     {
      action = TRADE_ACTION_PENDING;

      if(m_dis_in > 0.0 && check_stoplevel(price,ORDER_TYPE_BUY_STOP))
         tipo = ORDER_TYPE_BUY_STOP;
      else
         if(check_stoplevel(price,ORDER_TYPE_BUY_LIMIT,true))
            tipo = ORDER_TYPE_BUY_LIMIT;
     }

   double tp = (m_tp == 0.0) ? 0.00 : normalizar(price+check_conversao(_pts_tp,m_tp,price));
   double sl = (m_sl == 0.0) ? 0.00 : normalizar(price-check_conversao(_pts_sl,m_sl,price));

   if(m_alvos_sl2)
     {
      double price_sl = check_price(m_price_sl2_buy);
      double sl2 = normalizar(price_sl-check_conversao(_pts_cus,m_dis_sl2,price_sl));

      if(sl2 > 0.00)
         if(sl2 > sl || sl == 0.00)
            sl = sl2;
     }

   if(m_alvos_tp2)
     {
      double price_tp = check_price(m_price_tp2_buy);
      double tp2 = normalizar(price_tp+check_conversao(_pts_cus,m_dis_tp2,price_tp));

      if(tp2 > 0.00)
         if(tp2 < tp || tp == 0.00)
            tp = tp2;
     }

   if(sl > 0.00)
      if(sl >= price)
        {
         filtro_log("Stoploss inválido para compra");
         return false;
        }
      else
         if(!check_stoplevel(sl,ORDER_TYPE_SELL_STOP,true,price))
            return false;

   if(tp > 0.00)
      if(tp <= price)
        {
         filtro_log("Takeprofit inválido para compra");
         return false;
        }
      else
         if(!check_stoplevel(tp,ORDER_TYPE_SELL_LIMIT,true,price))
            return false;

   if(enviar_ordem(action,tipo,price,0,tp,sl,m_volume,"CIN#"))
     {
      filtro_log("Ordem de compra enviada com sucesso");
      return true;
     }
   else
      filtro_log("Falha no envio da abertura da compra");

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::enviar_venda(void)
  {
   if(!_vender)
      return false;

   if(!check_permissao())
      return false;

   if(!check_spread())
      return false;

   double bid = SymbolInfoDouble(M_SYMBOL,SYMBOL_BID);
   double price = (m_price_sell == 0 || !m_pendente_in) ? bid : check_price(m_price_sell);

   if(fabs(m_dis_in) > 0 && m_pendente_in)
      price = normalizar(price-check_conversao(_pts_inout,m_dis_in,price));

   ENUM_TRADE_REQUEST_ACTIONS action = TRADE_ACTION_DEAL;
   ENUM_ORDER_TYPE tipo = ORDER_TYPE_SELL;

   if(m_pendente_in)
     {
      action = TRADE_ACTION_PENDING;

      if(m_dis_in > 0.0 && check_stoplevel(price,ORDER_TYPE_SELL_STOP))
         tipo = ORDER_TYPE_SELL_STOP;
      else
         if(check_stoplevel(price,ORDER_TYPE_SELL_LIMIT,true))
            tipo = ORDER_TYPE_SELL_LIMIT;
     }

   double tp = (m_tp == 0) ? 0.00 : normalizar(price-check_conversao(_pts_tp,m_tp,price));
   double sl = (m_sl == 0) ? 0.00 : normalizar(price+check_conversao(_pts_sl,m_sl,price));

   if(m_alvos_sl2)
     {
      double price_sl = check_price(m_price_sl2_sell);
      double sl2 = normalizar(price_sl+check_conversao(_pts_cus,m_dis_sl2,price_sl));

      if(sl2 > 0.00)
         if(sl2 < sl || sl == 0.00)
            sl = sl2;
     }

   if(m_alvos_tp2)
     {
      double price_tp = check_price(m_price_tp2_sell);
      double tp2 = normalizar(price_tp-check_conversao(_pts_cus,m_dis_tp2,price_tp));

      if(tp2 > 0.00)
         if(tp2 > tp || tp == 0.00)
            tp = tp2;
     }

   if(sl > 0.00)
      if(sl <= price)
        {
         filtro_log("Stoploss inválido para venda");
         return false;
        }
      else
         if(!check_stoplevel(sl,ORDER_TYPE_BUY_STOP,true,price))
            return false;

   if(tp > 0.00)
      if(tp >= price)
        {
         filtro_log("Takeprofit inválido para venda");
         return false;
        }
      else
         if(!check_stoplevel(tp,ORDER_TYPE_BUY_LIMIT,true,price))
            return false;

   if(enviar_ordem(action,tipo,price,0,tp,sl,m_volume,"VIN#"))
     {
      filtro_log("Ordem de venda enviada com sucesso");
      return true;
     }
   else
      filtro_log("Falha no envio da abertura da venda");

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::enviar_saida(const double pos, const ulong ticket_out)
  {
   if(fabs(pos) > 0.00)
      if(!m_pendente_out)
        {
         zeragem_compulsoria();
         return true;
        }
      else
         if(ticket_out == 0)
           {
            if(!check_permissao())
               return false;

            double price;
            ENUM_ORDER_TYPE tipo;

            if(pos > 0.00)
              {
               double bid = check_price(m_price_out_buy);
               price = normalizar(bid+check_conversao(_pts_inout,m_dis_out,bid));
               tipo = (m_dis_out < 0.0) ? ORDER_TYPE_SELL_STOP : ORDER_TYPE_SELL_LIMIT;
              }
            else
              {
               double ask = check_price(m_price_out_sell);
               price = normalizar(ask-check_conversao(_pts_inout,m_dis_out,ask));
               tipo = (m_dis_out < 0.0) ? ORDER_TYPE_BUY_STOP : ORDER_TYPE_BUY_LIMIT;
              }

            if(check_stoplevel(price,tipo,true))
               return enviar_ordem(TRADE_ACTION_PENDING,tipo,price,0,0,0,fabs(pos),"OUT#");
           }
         else
            if(OrderSelect(ticket_out))
              {
               double vol = OrderGetDouble(ORDER_VOLUME_CURRENT);
               ENUM_ORDER_TYPE tipo = (ENUM_ORDER_TYPE)OrderGetInteger(ORDER_TYPE);

               if((pos < 0 && (tipo == ORDER_TYPE_SELL_LIMIT || tipo == ORDER_TYPE_SELL_STOP)) ||
                  (pos > 0 && (tipo == ORDER_TYPE_BUY_LIMIT || tipo == ORDER_TYPE_BUY_STOP)) || fabs(pos) != vol)
                  if(OrderGetInteger(ORDER_STATE) != ORDER_STATE_PARTIAL)
                     return enviar_ordem(TRADE_ACTION_REMOVE,tipo,OrderGetDouble(ORDER_PRICE_OPEN),ticket_out);
              }
            else
               filtro_log("Falha em selecionar a ordem de saída pendente");

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::breakeven_sl(const ulong ticket, const double price)
  {
   if(m_sl_be <= 0.0 || m_sl_be_dis <= 0.0)
      return false;

   if(!PositionSelectByTicket(ticket))
      return false;

   ENUM_POSITION_TYPE tipo = (ENUM_POSITION_TYPE)PositionGetInteger(POSITION_TYPE);
   double sl = PositionGetDouble(POSITION_SL);
   double tp = PositionGetDouble(POSITION_TP);
   double dis = check_conversao(_pts_sl,m_sl_be-m_sl_be_dis,price);
   double new_sl = sl;

   if(tipo == POSITION_TYPE_BUY)
     {
      double referencia = SymbolInfoDouble(M_SYMBOL,SYMBOL_BID);

      if(referencia >= price+check_conversao(_pts_sl,m_sl_be,price))
         if(sl == 0.0)
            new_sl = normalizar(price+dis);
         else
            if(normalizar(price+dis) > sl)
               new_sl = normalizar(price+dis);
     }
   else
     {
      double referencia = SymbolInfoDouble(M_SYMBOL,SYMBOL_ASK);

      if(referencia <= price-check_conversao(_pts_sl,m_sl_be,price))
         if(sl == 0.0)
            new_sl = normalizar(price-dis);
         else
            if(normalizar(price-dis) < sl)
               new_sl = normalizar(price-dis);
     }

   if(new_sl != sl)
     {
      string msg;
      StringConcatenate(msg,"Mover Breakeven SL de ",DoubleToString(sl,M_DIGITS)," para ",DoubleToString(new_sl,M_DIGITS));
      filtro_log(msg);
      return enviar_ordem(TRADE_ACTION_SLTP,(ENUM_ORDER_TYPE)tipo,price,ticket,tp,new_sl,0,PositionGetString(POSITION_COMMENT));
     }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::trailling_sl(const ulong ticket, const double price)
  {
   if(m_sl_ts <= 0 || m_sl_ts_step <= 0)
      return false;

   if(!PositionSelectByTicket(ticket))
      return false;

   ENUM_POSITION_TYPE tipo = (ENUM_POSITION_TYPE)PositionGetInteger(POSITION_TYPE);
   double sl = PositionGetDouble(POSITION_SL);
   double tp = PositionGetDouble(POSITION_TP);
   double dis = (m_sl_ts+m_sl);

   if(m_sl_be > 0 && m_sl_be_dis > 0)
      dis = (m_sl_ts >= m_sl_be) ? (m_sl_ts-m_sl_be+m_sl_be_dis) : (m_sl_be-m_sl_be_dis);

   double new_sl = sl;
   dis = check_conversao(_pts_sl,dis,price);

   if(tipo == POSITION_TYPE_BUY)
     {
      double referencia = SymbolInfoDouble(M_SYMBOL,SYMBOL_BID);

      if(referencia >= price+check_conversao(_pts_sl,m_sl_ts,price))
         if(sl == 0.0)
            new_sl = normalizar(price);
         else
            if(normalizar(referencia-dis) > sl)
              {
               new_sl += check_conversao(_pts_sl,m_sl_ts_step,price);
               new_sl = normalizar(new_sl);
              }
     }
   else
     {
      double referencia = SymbolInfoDouble(M_SYMBOL,SYMBOL_ASK);

      if(referencia <= price-check_conversao(_pts_sl,m_sl_ts,price))
         if(sl == 0.0)
            new_sl = normalizar(price);
         else
            if(normalizar(referencia+dis) < sl)
              {
               new_sl -= check_conversao(_pts_sl,m_sl_ts_step,price);
               new_sl = normalizar(new_sl);
              }
     }

   if(new_sl != sl)
     {
      string msg;
      StringConcatenate(msg,"Mover Trailling stop de ",DoubleToString(sl,M_DIGITS)," para ",DoubleToString(new_sl,M_DIGITS));
      filtro_log(msg);
      return enviar_ordem(TRADE_ACTION_SLTP,(ENUM_ORDER_TYPE)tipo,price,ticket,tp,new_sl,0,PositionGetString(POSITION_COMMENT));
     }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::breakeven_tp(const ulong ticket, const double price)
  {
   if(m_tp_be <= 0.0 || m_tp_be_dis <= 0.0)
      return false;

   if(!PositionSelectByTicket(ticket))
      return false;

   ENUM_POSITION_TYPE tipo = (ENUM_POSITION_TYPE)PositionGetInteger(POSITION_TYPE);
   double sl = PositionGetDouble(POSITION_SL);
   double tp = PositionGetDouble(POSITION_TP);
   double dis = check_conversao(_pts_tp,m_tp_be-m_tp_be_dis,price);
   double new_tp = tp;

   if(tipo == POSITION_TYPE_SELL)
     {
      double referencia = SymbolInfoDouble(M_SYMBOL,SYMBOL_ASK);

      if(referencia >= price+check_conversao(_pts_tp,m_tp_be,price))
         if(tp == 0.0)
            new_tp = normalizar(price+dis);
         else
            if(normalizar(price+dis) > tp)
               new_tp = normalizar(price+dis);
     }
   else
     {
      double referencia = SymbolInfoDouble(M_SYMBOL,SYMBOL_BID);

      if(referencia <= price-check_conversao(_pts_tp,m_tp_be,price))
         if(tp == 0.0)
            new_tp = normalizar(price-dis);
         else
            if(normalizar(price-dis) < tp)
               new_tp = normalizar(price-dis);
     }

   if(new_tp != tp)
     {
      string msg;
      StringConcatenate(msg,"Mover Breakeven TP de ",DoubleToString(tp,M_DIGITS)," para ",DoubleToString(new_tp,M_DIGITS));
      filtro_log(msg);
      return enviar_ordem(TRADE_ACTION_SLTP,(ENUM_ORDER_TYPE)tipo,price,ticket,new_tp,sl,0,PositionGetString(POSITION_COMMENT));
     }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::trailling_tp(const ulong ticket, const double price)
  {
   if(m_tp_ts <= 0 || m_tp_ts_step <= 0)
      return false;

   if(!PositionSelectByTicket(ticket))
      return false;

   ENUM_POSITION_TYPE tipo = (ENUM_POSITION_TYPE)PositionGetInteger(POSITION_TYPE);
   double sl = PositionGetDouble(POSITION_SL);
   double tp = PositionGetDouble(POSITION_TP);
   double dis = (m_tp_ts+m_tp);

   if(m_tp_be > 0 && m_tp_be_dis > 0)
      dis = (m_tp_ts >= m_tp_be) ? (m_tp_ts-m_tp_be+m_tp_be_dis) : (m_tp_be-m_tp_be_dis);

   double new_tp = tp;
   dis = check_conversao(_pts_tp,dis,price);

   if(tipo == POSITION_TYPE_SELL)
     {
      double referencia = SymbolInfoDouble(M_SYMBOL,SYMBOL_ASK);

      if(referencia >= price+check_conversao(_pts_tp,m_tp_ts,price))
         if(tp == 0.00)
            new_tp = normalizar(price);
         else
            if(normalizar(referencia-dis) > tp)
              {
               new_tp += check_conversao(_pts_tp,m_tp_ts_step,price);
               new_tp = normalizar(new_tp);
              }
     }
   else
     {
      double referencia = SymbolInfoDouble(M_SYMBOL,SYMBOL_BID);

      if(referencia <= price-check_conversao(_pts_tp,m_tp_ts,price))
         if(tp == 0.0)
            new_tp = normalizar(price);
         else
            if(normalizar(referencia+dis) < tp)
              {
               new_tp -= check_conversao(_pts_tp,m_tp_ts_step,price);
               new_tp = normalizar(new_tp);
              }
     }

   if(new_tp != tp)
     {
      string msg;
      StringConcatenate(msg,"Mover Trailling profit de ",DoubleToString(tp,M_DIGITS)," para ",DoubleToString(new_tp,M_DIGITS));
      filtro_log(msg);
      return enviar_ordem(TRADE_ACTION_SLTP,(ENUM_ORDER_TYPE)tipo,price,ticket,new_tp,sl,0,PositionGetString(POSITION_COMMENT));
     }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::check_alvos(const double pos, const ulong ticket, const double primeira, const double medio)
  {
   double price_sl = (_medio_sl) ? medio : primeira;
   double price_tp = (_medio_tp) ? medio : primeira;

   if(fabs(pos) > m_volume)
      if(PositionSelectByTicket(ticket))
        {
         double sl = PositionGetDouble(POSITION_SL);
         double tp = PositionGetDouble(POSITION_TP);
         double entrada = PositionGetDouble(POSITION_PRICE_OPEN);
         string coment = PositionGetString(POSITION_COMMENT);
         ENUM_ORDER_TYPE tipo = (pos > 0) ? ORDER_TYPE_BUY : ORDER_TYPE_SELL;

         if(m_sl > 0 && _repo_sl)
           {
            double conversao = check_conversao(_pts_sl,m_sl,price_sl);
            double ajuste_sl = (pos > 0) ? normalizar(price_sl-conversao) : normalizar(price_sl+conversao);

            if((sl < ajuste_sl && pos > 0) || (sl > ajuste_sl && pos < 0) || sl == 0.00)
               return enviar_ordem(TRADE_ACTION_SLTP,tipo,entrada,ticket,tp,ajuste_sl,fabs(pos),coment);
           }

         if(m_tp > 0 && _repo_tp)
           {
            double conversao = check_conversao(_pts_tp,m_tp,price_tp);
            double ajuste_tp = (pos > 0) ? normalizar(price_tp+conversao) : normalizar(price_tp-conversao);

            if((tp < ajuste_tp && pos < 0) || (tp > ajuste_tp && pos > 0) || tp == 0.00)
               return enviar_ordem(TRADE_ACTION_SLTP,tipo,entrada,ticket,ajuste_tp,sl,fabs(pos),coment);
           }
        }

   if(!breakeven_sl(ticket,price_sl))
      trailling_sl(ticket,price_sl);

   if(!breakeven_tp(ticket,price_tp))
      trailling_tp(ticket,price_tp);

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::enviar_ordem(const ENUM_TRADE_REQUEST_ACTIONS action,
                            const ENUM_ORDER_TYPE tipo,
                            double price=0,
                            ulong  ticket=0,
                            double tp=0,
                            double sl=0,
                            double lot=0,
                            string coment=NULL,
                            ulong ticket_by=0)
  {
   MqlTradeRequest request;
   MqlTradeResult  result;
   MqlTradeCheckResult check;

   ZeroMemory(request);
   ZeroMemory(result);
   ZeroMemory(check);
   ResetLastError();

   if(action == TRADE_ACTION_PENDING || action == TRADE_ACTION_MODIFY)
      if(!check_expiration(request.type_time))
        {
         filtro_log("Falha ao atribuir uma expiração válida");
         return false;
        }

   if(action == TRADE_ACTION_DEAL || action == TRADE_ACTION_PENDING)
      if(!check_filling(action,request.type_filling))
        {
         filtro_log("Falha ao atribuir preenchimento para o envio da ordem");
         return false;
        }

   if(action == TRADE_ACTION_REMOVE || action == TRADE_ACTION_MODIFY)
      request.order = ticket;
   else
     {
      request.position = ticket;
      request.position_by = ticket_by;
     }

   request.action    = action;
   request.symbol    = M_SYMBOL;
   request.volume    = lot;
   request.type      = tipo;
   request.price     = normalizar(price);
   request.deviation = 10;
   request.magic     = m_magic;
   request.comment   = coment+Expert;
   request.tp        = tp;
   request.sl        = sl;

   switch(action)
     {
      case TRADE_ACTION_DEAL:
         filtro_log("Solicitado envio de ordem a mercado");
         break;
      case TRADE_ACTION_PENDING:
         filtro_log("Solicitado abertura de ordem pendente");
         break;
      case TRADE_ACTION_SLTP:
         filtro_log("Solicitado modificação do SL e/ou TP");
         break;
      case TRADE_ACTION_MODIFY:
         filtro_log("Solicitado modficiação de ordem pendente");
         break;
      case TRADE_ACTION_REMOVE:
         filtro_log("Solicitado remoção de ordem pendente");
         break;
      case TRADE_ACTION_CLOSE_BY:
         filtro_log("Solicitado fechamento pela oposta");
         break;
     }

   if(!OrderCheck(request,check))
     {
      filtro_log(StringFormat("Erro %d na checagem da ordem",GetLastError()));
      filtro_log(StringFormat("Retorno %d (%s)",check.retcode,check.comment));
      return false;
     }

   if(!OrderSend(request,result))
     {
      filtro_log(StringFormat("Erro %d no envio da ordem",GetLastError()));
      filtro_log(StringFormat("Retorno %d (%s)",result.retcode,result.comment));
      return false;
     }

   filtro_log(StringFormat("Ordem enviada. %d (%s)",result.retcode,result.comment));
   string msg = NULL;

   if(result.deal > 0)
      msg = StringFormat("Negócio #%I64u. ",result.deal);

   if(result.order > 0)
      msg += StringFormat("Ordem #%I64u",result.order);

   if(msg != NULL)
      filtro_log(msg);

   return true;
  }
//+------------------------------------------------------------------+
//| Função de zerar                                                  |
//+------------------------------------------------------------------+
void EXECUCAO::zeragem_compulsoria(void)
  {
   for(int i=PositionsTotal()-1; i>=0; i--)
     {
      ulong ticket = PositionGetTicket(i);
      PositionSelectByTicket(ticket);

      if(PositionGetString(POSITION_SYMBOL) != M_SYMBOL)
         continue;

      if(PositionGetInteger(POSITION_MAGIC) != m_magic)
         continue;

      ENUM_POSITION_TYPE tipo = (ENUM_POSITION_TYPE)PositionGetInteger(POSITION_TYPE);
      double vol = PositionGetDouble(POSITION_VOLUME);

      if(check_permissao())
         if(tipo == POSITION_TYPE_BUY)
           {
            if(enviar_ordem(TRADE_ACTION_DEAL,ORDER_TYPE_SELL,SymbolInfoDouble(M_SYMBOL,SYMBOL_BID),ticket,0,0,vol,"OUT#"))
              {
               string msg = "Encerrada COMPRA "+IntegerToString(ticket)+" e volume "+DoubleToString(vol,_vol_digitos);
               filtro_log(msg);
              }
           }
         else
           {
            if(enviar_ordem(TRADE_ACTION_DEAL,ORDER_TYPE_BUY,SymbolInfoDouble(M_SYMBOL,SYMBOL_ASK),ticket,0,0,vol,"OUT#"))
              {
               string msg = "Encerrada VENDA "+IntegerToString(ticket)+" e volume "+DoubleToString(vol,_vol_digitos);
               filtro_log(msg);
              }
           }
     }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::check_pendentes(const s_position &pos, const s_ordem &ord, const s_history &his)
  {
   if(pos.volume == 0.00)
      return false;

   confirmar_aumento(false,pos.volume,his.entrada,pos.sl,pos.tp,m_af1_dis,m_af1_lot,ord.af1,his.af1,"AF1#");
   confirmar_aumento(false,pos.volume,his.entrada,pos.sl,pos.tp,m_af2_dis,m_af2_lot,ord.af2,his.af2,"AF2#");
   confirmar_aumento(false,pos.volume,his.entrada,pos.sl,pos.tp,m_af3_dis,m_af3_lot,ord.af3,his.af3,"AF3#");
   confirmar_aumento(false,pos.volume,his.entrada,pos.sl,pos.tp,m_af4_dis,m_af4_lot,ord.af4,his.af4,"AF4#");
   confirmar_aumento(false,pos.volume,his.entrada,pos.sl,pos.tp,m_af5_dis,m_af5_lot,ord.af5,his.af5,"AF5#");

   confirmar_aumento(true,pos.volume,his.entrada,pos.sl,pos.tp,m_ac1_dis,m_ac1_lot,ord.ac1,his.ac1,"AC1#");
   confirmar_aumento(true,pos.volume,his.entrada,pos.sl,pos.tp,m_ac2_dis,m_ac2_lot,ord.ac2,his.ac2,"AC2#");
   confirmar_aumento(true,pos.volume,his.entrada,pos.sl,pos.tp,m_ac3_dis,m_ac3_lot,ord.ac3,his.ac3,"AC3#");
   confirmar_aumento(true,pos.volume,his.entrada,pos.sl,pos.tp,m_ac4_dis,m_ac4_lot,ord.ac4,his.ac4,"AC4#");
   confirmar_aumento(true,pos.volume,his.entrada,pos.sl,pos.tp,m_ac5_dis,m_ac5_lot,ord.ac5,his.ac5,"AC5#");

   double parcial = (_medio_pn) ? his.medio : his.entrada;
   confirmar_parciais(pos.volume,parcial,m_p1_dis,m_p1_lot,ord.p1,his.p1,"SP1#");
   confirmar_parciais(pos.volume,parcial,m_p2_dis,m_p2_lot,ord.p2,his.p2,"SP2#");
   confirmar_parciais(pos.volume,parcial,m_p3_dis,m_p3_lot,ord.p3,his.p3,"SP3#");
   confirmar_parciais(pos.volume,parcial,m_p4_dis,m_p4_lot,ord.p4,his.p4,"SP4#");

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void EXECUCAO::confirmar_aumento(const bool contra, const double pos, const double entrada, const double sl, const double tp,
                                 const double dis, const double lot, const ulong ticket, const ulong history, const string nome)
  {
   if(entrada > 0.00)
      if(dis > 0.00 && lot > 0.00)
         if(ticket == 0 && history == 0)
           {
            ENUM_ORDER_TYPE tipo = (pos > 0.00) ? ORDER_TYPE_BUY_STOP : ORDER_TYPE_SELL_STOP;
            bool pts = (contra) ? _pts_ac : _pts_af;
            double conversao = check_conversao(pts,dis,entrada);
            double price = ((pos > 0.00 && !contra) || (pos < 0.00 && contra)) ? entrada+conversao : entrada-conversao;

            if(contra)
               tipo = (pos > 0.00) ? ORDER_TYPE_BUY_LIMIT : ORDER_TYPE_SELL_LIMIT;

            if(tipo ==  ORDER_TYPE_BUY_STOP || tipo ==  ORDER_TYPE_BUY_LIMIT)
              {
               if((price >= tp && tp > 0.00) || price <= sl)
                  return;
              }
            else
               if(price <= tp || (price >= sl && sl > 0.00))
                  return;

            if(check_stoplevel(price,tipo))
               if(check_permissao())
                  enviar_ordem(TRADE_ACTION_PENDING,tipo,price,0,tp,sl,lot,nome);
           }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void EXECUCAO::confirmar_parciais(const double pos, const double price, const double dis, const double lot,
                                  const ulong ticket, const ulong history, const string nome)
  {
   if(price > 0.00)
      if(fabs(dis) > 0.00 && lot > 0.00)
         if(history == 0)
           {
            double conversao = check_conversao(_pts_pn,fabs(dis),price);
            double parcial = ((pos > 0 && dis > 0) || (pos < 0 && dis < 0)) ? normalizar(price+conversao) : normalizar(price-conversao);
            double vol = (lot > fabs(pos)) ? fabs(pos) : lot;
            ENUM_ORDER_TYPE tipo;

            if(pos > 0.00)
               tipo = (dis > 0) ? ORDER_TYPE_SELL_LIMIT : ORDER_TYPE_SELL_STOP;
            else
               tipo = (dis > 0) ? ORDER_TYPE_BUY_LIMIT : ORDER_TYPE_BUY_STOP;

            if(ticket > 0)
              {
               if(OrderSelect(ticket))
                 {
                  double volume = OrderGetDouble(ORDER_VOLUME_CURRENT);

                  if(tipo == OrderGetInteger(ORDER_TYPE))
                     if(volume > fabs(pos) || (volume < fabs(pos) && volume < lot))
                       {
                        if(OrderGetInteger(ORDER_STATE) != ORDER_STATE_PARTIAL)
                           enviar_ordem(TRADE_ACTION_REMOVE,tipo,0,ticket);
                       }
                     else
                        if(OrderGetDouble(ORDER_PRICE_OPEN) != parcial)
                           if(check_stoplevel(parcial,tipo))
                              enviar_ordem(TRADE_ACTION_MODIFY,tipo,parcial,ticket,0,0,volume,OrderGetString(ORDER_COMMENT));
                 }
              }
            else
               if(check_stoplevel(parcial,tipo))
                  if(check_permissao())
                     enviar_ordem(TRADE_ACTION_PENDING,tipo,parcial,0,0,0,vol,nome);
           }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::check_gradiente_linear(const double posicao, const double entrada, const int &grad_qtd[], const ulong &grad_ticket[], const ulong last, const double sl)
  {
   string comentario = HistoryDealGetString(last,DEAL_COMMENT);
   int id = (last > 0) ? (int)StringSubstr(comentario,4,StringFind(comentario,"#",4)-4) : 0;
   datetime ultima = 0;

   if(last > 0 && m_gra_tp > 0.0)
     {
      ulong ticket = grad_ticket[0];
      double vol = HistoryDealGetDouble(last,DEAL_VOLUME);
      double price = HistoryDealGetDouble(last,DEAL_PRICE);
      double conv_tp = check_conversao(_pts_grad,m_gra_tp,price);
      double tp = (posicao > 0) ? normalizar(price+conv_tp) : normalizar(price-conv_tp);
      ENUM_ORDER_TYPE tipo = (posicao > 0) ? ORDER_TYPE_SELL_LIMIT : ORDER_TYPE_BUY_LIMIT;
      ultima = (datetime)HistoryDealGetInteger(last,DEAL_TIME);

      if(ticket > 0)
         if(OrderSelect(ticket))
           {
            double parcial = OrderGetDouble(ORDER_PRICE_OPEN);

            if(tp == 0 || (posicao > 0 && parcial > tp) || (posicao < 0 && parcial < tp))
               if(enviar_ordem(TRADE_ACTION_REMOVE,tipo,0,ticket))
                  ticket = 0;
           }

      if(ticket == 0 && vol > 0.0)
         if(check_stoplevel(tp,tipo))
            if(check_permissao())
               enviar_ordem(TRADE_ACTION_PENDING,tipo,tp,0,0,0,vol,"GTP#");
     }

   for(int i=id+1; i<=m_grad_qtd; i++)
     {
      double price = 0.0;
      string nome = NULL;
      ulong ticket = grad_ticket[i];
      ENUM_ORDER_TYPE tipo = (posicao > 0) ? ORDER_TYPE_BUY_LIMIT : ORDER_TYPE_SELL_LIMIT;

      if(OrderSelect(ticket))
        {
         if(m_grad_ajuste > 0)
            if(last > 0 && ultima > 0)
               if(ultima > OrderGetInteger(ORDER_TIME_SETUP))
                  if(OrderGetInteger(ORDER_STATE) != ORDER_STATE_PARTIAL)
                     enviar_ordem(TRADE_ACTION_REMOVE,tipo,0,ticket);
        }
      else
         if(grad_qtd[i] < m_grad_max)
           {
            double conv = check_conversao(_pts_grad,m_gra_dis*i,entrada);
            double ajuste = check_conversao(_pts_grad,m_grad_ajuste,entrada);
            ajuste *= grad_qtd[0];

            price = (posicao > 0) ? normalizar(entrada-conv-ajuste) : normalizar(entrada+conv+ajuste);
            StringConcatenate(nome,"GIN#",IntegerToString(i),"#");
           }

      if(price > 0 && nome != NULL)
         if(sl == 0.0 || (posicao > 0 && price > sl) || (posicao < 0 && price < sl))
            if(check_stoplevel(price,tipo))
               if(check_permissao())
                  enviar_ordem(TRADE_ACTION_PENDING,tipo,price,0,0,0,m_grad_vol,nome);
     }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::check_saida_temporal(const datetime hora, const double lucro)
  {
   int espera = m_temporal_pos_time;
   double max = m_temporal_pos_max;
   double min = m_temporal_pos_min;

   if(lucro < 0.00)
     {
      espera = m_temporal_neg_time;
      max = m_temporal_neg_max;
      min = m_temporal_neg_min;
     }

   if(espera <= 0)
      return false;

   if(fabs(max) > 0.00 && fabs(lucro) > fabs(max))
      return false;

   if(fabs(min) > 0.00 && fabs(lucro) < fabs(min))
      return false;

   if(check_temporizador(hora,espera,m_temporal_ref))
     {
      zeragem_compulsoria();
      return true;
     }

   return false;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::check_filtro_barra(void)
  {
   MqlRates rates[];
   ZeroMemory(rates);
   ArraySetAsSeries(rates,true);

   if(CopyRates(M_SYMBOL,m_candle_tf,0,1,rates) < 1)
     {
      filtro_log("Falha em conferir o filtro de vela");
      return false;
     }

   double vela = NormalizeDouble((rates[0].high-rates[0].low)/M_POINT,0);
   double corpo = NormalizeDouble((rates[0].close-rates[0].open)/M_POINT,0);

   if(vela >= m_candle_min)
      if(vela < m_candle_max || m_candle_max == 0)
         if(fabs(corpo) >= m_corpo_min)
            if(fabs(corpo) < m_corpo_max || m_corpo_max == 0)
               return true;

   string msg = "Bloqueio por filtro de vela";
   filtro_log(msg);
   update_painel_descritivo(msg);
   return false;
  }
//+------------------------------------------------------------------+
//| Normalizar Preço                                                 |
//+------------------------------------------------------------------+
double EXECUCAO::normalizar(const double price)
  {
   double size = SymbolInfoDouble(M_SYMBOL,SYMBOL_TRADE_TICK_SIZE);

   if(size != 0.00)
      return(NormalizeDouble(MathRound(price/size)*size,M_DIGITS));

   return(NormalizeDouble(price,M_DIGITS));
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool EXECUCAO::check_procura_sinal(const bool compra, const bool saida, const datetime ultima)
  {
   bool usar = (saida) ? m_sinais_out : m_sinais_in;

   if(usar)
     {
      int max = (saida) ? _max_sell_out : _max_sell_in;

      if(compra)
         max = (saida) ? _max_buy_out : _max_buy_in;

      if(iTime(M_SYMBOL,m_timeframe,max) <= ultima)
        {
         string msg = "Aguardando liberação para buscar sinais";
         filtro_log(msg);
         update_painel_descritivo(msg);
         return false;
        }
     }

   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
bool PROCESSAR::iniciando(void)
  {
   ChartSetSymbolPeriod(0,_Symbol,m_timeframe);
   Sleep(300);

   _prefix_linha = Robot+"_LINHA_";
   _prefix_painel = Robot+"_PAINEL";
   _boleta = m_volume;
   _visual = false;
   _operar = true;
   
   if(!criar_log())
     {
      filtro_log("Falha ao criar as linhas do log");
      return false;
     }

   if(!check_ativo())
     {
      filtro_log("Falha em atribuir o ativo para cross order");
      return false;
     }

   if(m_sinais_in)
      if(m_compra_in > 0 || m_venda_in > 0)
        {
         filtro_log("Procura na vela seguinte na entrada inválido");
         filtro_log("Só pode ser usado com o sinal de entrada 1");
         return false;
        }

   if(m_sinais_out)
      if(m_compra_out > 0 || m_venda_out > 0)
        {
         filtro_log("Procura na vela seguinte na saída inválido");
         filtro_log("Só pode ser usado com o sinal de saída 1");
         return false;
        }

   check_visual();
   check_globais();

   if(m_inverte_in)
     {
      int inverter = _max_sell_in;
      _max_sell_in = _max_buy_in;
      _max_buy_in = inverter;
     }

   if(m_inverte_out)
     {
      int inverter = _max_sell_out;
      _max_sell_out = _max_buy_out;
      _max_buy_out = inverter;
     }

   if(!verificar_licenca())
     {
      filtro_log("Sem permissão de licença para esta conta");
      return false;
     }

   _vol_digitos = -1;

   if(!check_volumes())
     {
      filtro_log("Falha na verificação de volume");
      return false;
     }

   if(!criar_painel())
     {
      filtro_log("Falha em iniciar o painel gráfico");
      return false;
     }

   if(!check_indicadores())
     {
      filtro_log("Falha em iniciar os indicadores");
      return false;
     }

   EventSetTimer(1);
   _atualizar = true;

   int   grad_qtd[];
   ulong grad_ticket[];

   ArrayResize(grad_qtd,m_grad_qtd+1);
   ArrayResize(grad_ticket,m_grad_qtd+1);
   ZeroMemory(grad_qtd);
   ZeroMemory(grad_ticket);

   set_horario();
   set_grafico();
   s_position pos = posicao();
   s_ordem ord = ordens(grad_ticket,pos.hora,pos.tp,pos.sl);
   s_history his = historico(grad_qtd,pos.hora);

   update_painel_position(pos);
   update_painel_history(his);
   gerenciar_linhas(pos,ord,grad_ticket,his.entrada,his.medio);

   ChartRedraw();
   ResetLastError();

   filtro_log(Expert+" Iniciado com sucesso em "+M_SYMBOL);
   return true;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void PROCESSAR::desligando(void)
  {
   excluir_indicadores();
   ObjectsDeleteAll(0,Robot,0);
   EventKillTimer();
   ChartSetInteger(0,CHART_SHOW_TRADE_LEVELS,true);
   ChartSetInteger(0,CHART_DRAG_TRADE_LEVELS,true);
   ChartSetInteger(0,CHART_COLOR_STOP_LEVEL,clrRed);
   ChartSetInteger(0,CHART_COLOR_VOLUME,clrLimeGreen);
   ChartRedraw();
   filtro_log("Expert removido completamente");
   Sleep(500);
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void PROCESSAR::processar_posicionado(const s_position &pos, const s_ordem &ord, const s_history &his, const int &grad_qtd[], const ulong &grad_ticket[])
  {
   check_alvos(pos.volume,pos.ticket,his.entrada,his.medio);
   check_pendentes(pos,ord,his);
   check_gradiente_linear(pos.volume,his.entrada,grad_qtd,grad_ticket,his.last,pos.sl);
   update_painel_descritivo("Em operação");

   if(_teste)
      if(m_tarjas && _visual)
         processar_grafico(CHARTEVENT_CHART_CHANGE,0,0,NULL);

   if(check_metas(his.saldo,pos.lucro,his.max,his.min))
     {
      zeragem_compulsoria();
      filtro_log("Zeragem por meta durante posição");
     }
   else
      if(!check_barra(false,pos.hora))
         update_painel_descritivo("Barra bloqueada para saída por execução");
      else
         if(check_saida_temporal(pos.hora,pos.lucro))
            filtro_log("Acionado saída por tempo");
         else
            if(!check_espera(pos.hora,m_espera_out))
               update_painel_descritivo("Aguardando tempo minímo para procurar saída");
            else
               if(pos.volume > 0.00)
                 {
                  if(check_procura_sinal(true,true,his.ult_time))
                    {
                     bool saida_compra = (m_inverte_out) ? check_saida_venda() : check_saida_compra();

                     if(saida_compra)
                        enviar_saida(pos.volume,ord.out);
                    }
                 }
               else
                  if(check_procura_sinal(false,true,his.ult_time))
                    {
                     bool saida_venda = (m_inverte_out) ? check_saida_compra() : check_saida_venda();

                     if(saida_venda)
                        enviar_saida(pos.volume,ord.out);
                    }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void PROCESSAR::processar_zerado(const s_history &his, ulong &grad_ticket[])
  {
   s_ordem ord = ordens(grad_ticket,0);

   if(!check_metas(his.saldo,0,his.max,his.min))
      if(!horario_operacional())
         update_painel_descritivo("Fora do horário operacional");
      else
         if(horario_espera())
            update_painel_descritivo("Pausa no horário operacional");
         else
            if(!check_barra(true,his.ult_time))
               update_painel_descritivo("Barra bloqueada para entrada por execução");
            else
               if(!check_espera(his.ult_time,m_espera_in))
                  update_painel_descritivo("Aguardando tempo minímo para procurar entrada");
               else
                  if(check_filtro_barra())
                    {
                     update_painel_descritivo("Procurando novas entradas");
                     bool comprar = false, vender = false;

                     if(check_procura_sinal(false,false,his.ult_time))
                        vender = (m_inverte_in) ? check_entrada_compra() : check_entrada_venda();

                     if(vender)
                       {
                        if(ord.buy > 0)
                          {
                           if(_cancel_oposto)
                              enviar_ordem(TRADE_ACTION_REMOVE,ORDER_TYPE_BUY,0,ord.buy);
                          }
                        else
                           if(ord.sell == 0)
                              enviar_venda();

                        return;
                       }

                     if(check_procura_sinal(true,false,his.ult_time))
                        comprar = (m_inverte_in) ? check_entrada_venda() : check_entrada_compra();

                     if(comprar)
                        if(ord.sell > 0)
                          {
                           if(_cancel_oposto)
                              enviar_ordem(TRADE_ACTION_REMOVE,ORDER_TYPE_SELL,0,ord.sell);
                          }
                        else
                           if(ord.buy == 0)
                              enviar_compra();
                    }
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void PROCESSAR::processando(void)
  {
   static int grad_qtd[];
   static ulong grad_ticket[];

   if(ArraySize(grad_ticket) <= m_grad_qtd)
     {
      ArrayResize(grad_qtd,m_grad_qtd+1);
      ArrayResize(grad_ticket,m_grad_qtd+1);
     }

   s_position pos = posicao();
   s_ordem ord = ordens(grad_ticket,pos.hora,pos.tp,pos.sl);
   s_history his = historico(grad_qtd,pos.hora);
   gerenciar_linhas(pos,ord,grad_ticket,his.entrada,his.medio);

   if(!_operar)
     {
      update_painel_descritivo("Expert desabilitado pelo usuário");
      return;
     }

   if(check_conexao())
      if(check_ticks())
         if(horario_zeragem())
           {
            if(fabs(pos.volume) > 0.00)
               zeragem_compulsoria();

            ordens(grad_ticket,0);
            update_painel_descritivo("Horário de zeragem compulsória");
           }
         else
            if(pos.volume == 0.00)
               processar_zerado(his,grad_ticket);
            else
               processar_posicionado(pos,ord,his,grad_qtd,grad_ticket);
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
int OnInit(void)
  {
   if(!in_pro.iniciando())
     {
      MessageBox("Consulte na aba diário e na aba expert os detalhes do erro","FALHA NA INICIALIZAÇÃO!",MB_OK);
      return INIT_FAILED;
     }

   return INIT_SUCCEEDED;
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void OnDeinit(const int reason)
  {
   in_pro.desligando();
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void OnTimer(void)
  {
   in_pro.atualizar_hora();
   if(m_processo == es_seg)
      in_pro.processando();
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void OnTick(void)
  {
   if(m_processo == es_tick)
      in_pro.processando();
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void OnTrade()
  {
   in_pro._atualizar = true;
   in_pro.processando();
  }
//+------------------------------------------------------------------+
//|                                                                  |
//+------------------------------------------------------------------+
void OnChartEvent(const int id, const long& lparam, const double& dparam, const string& sparam)
  {
   in_pro.processar_grafico(id,lparam,dparam,sparam);
  }
//+------------------------------------------------------------------+
