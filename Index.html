import os
from datetime import datetime
import pandas as pd
import streamlit as st

from reportlab.lib.pagesizes import A4
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer, Table, TableStyle
from reportlab.lib.styles import getSampleStyleSheet, ParagraphStyle
from reportlab.lib import colors

# Configuração da Página do Streamlit
st.set_page_config(
    page_title="Gerador de Recibos e Relatórios",
    page_icon="🧾",
    layout="wide"
)

# Inicialização do Banco de Dados em Sessão (Simulado)
if "sales_data" not in st.session_state:
    st.session_state.sales_data = pd.DataFrame(columns=[
        "ID", "Data", "Cliente", "Produto", "Quantidade", "Valor Unitário", "Total"
    ])

# Função para Gerar PDF de Relatório de Vendas
def generate_sales_report_pdf(df_filtered, start_date, end_date):
    pdf_path = "relatorio_vendas.pdf"
    doc = SimpleDocTemplate(pdf_path, pagesize=A4, rightMargin=30, leftMargin=30, topMargin=30, bottomMargin=30)
    elements = []
    
    styles = getSampleStyleSheet()
    title_style = ParagraphStyle(
        'TitleStyle',
        parent=styles['Heading1'],
        fontSize=18,
        textColor=colors.HexColor('#1f2937'),
        alignment=1, # Centralizado
        spaceAfter=15
    )
    subtitle_style = ParagraphStyle(
        'SubtitleStyle',
        parent=styles['Normal'],
        fontSize=10,
        textColor=colors.HexColor('#4b5563'),
        alignment=1,
        spaceAfter=20
    )
    
    # Cabeçalho
    elements.append(Paragraph("<b>Relatório de Produtos Vendidos</b>", title_style))
    period_str = f"Período: {start_date.strftime('%d/%m/%Y')} a {end_date.strftime('%d/%m/%Y')}"
    elements.append(Paragraph(period_str, subtitle_style))
    elements.append(Spacer(1, 10))
    
    # Tabela de Dados
    table_data = [["Data", "Cliente", "Produto", "Qtd", "Unitário", "Total"]]
    for _, row in df_filtered.iterrows():
        table_data.append([
            str(row["Data"]),
            str(row["Cliente"]),
            str(row["Produto"]),
            str(row["Quantidade"]),
            f"R$ {row['Valor Unitário']:.2f}",
            f"R$ {row['Total']:.2f}"
        ])
        
    t = Table(table_data, colWidths=[70, 110, 140, 40, 65, 65])
    t.setStyle(TableStyle([
        ('BACKGROUND', (0,0), (-1,0), colors.HexColor('#3b82f6')),
        ('TEXTCOLOR', (0,0), (-1,0), colors.whitesmoke),
        ('ALIGN', (0,0), (-1,-1), 'CENTER'),
        ('FONTNAME', (0,0), (-1,0), 'Helvetica-Bold'),
        ('FONTSIZE', (0,0), (-1,0), 10),
        ('BOTTOMPADDING', (0,0), (-1,0), 8),
        ('BACKGROUND', (0,1), (-1,-1), colors.HexColor('#f9fafb')),
        ('GRID', (0,0), (-1,-1), 0.5, colors.HexColor('#d1d5db')),
        ('FONTSIZE', (0,1), (-1,-1), 9),
    ]))
    
    elements.append(t)
    elements.append(Spacer(1, 15))
    
    # Totalizador no PDF
    total_faturamento = df_filtered["Total"].sum() if not df_filtered.empty else 0.0
    total_itens = df_filtered["Quantidade"].sum() if not df_filtered.empty else 0
    
    summary_text = f"<b>Total de Itens Vendidos:</b> {total_itens} | <b>Faturamento Total:</b> R$ {total_faturamento:.2f}"
    summary_style = ParagraphStyle('SummaryStyle', parent=styles['Normal'], fontSize=11, textColor=colors.HexColor('#111827'), alignment=2)
    elements.append(Paragraph(summary_text, summary_style))
    
    doc.build(elements)
    return pdf_path

# Função para Gerar Recibo Individual em PDF
def generate_receipt_pdf(receipt_data):
    pdf_path = f"recibo_{receipt_data['ID']}.pdf"
    doc = SimpleDocTemplate(pdf_path, pagesize=A4, rightMargin=40, leftMargin=40, topMargin=40, bottomMargin=40)
    elements = []
    
    styles = getSampleStyleSheet()
    title_style = ParagraphStyle('ReciboTitle', parent=styles['Heading1'], fontSize=20, textColor=colors.HexColor('#1e3a8a'), alignment=1, spaceAfter=10)
    normal_style = ParagraphStyle('ReciboNormal', parent=styles['Normal'], fontSize=12, textColor=colors.HexColor('#374151'), spaceAfter=8)
    
    elements.append(Paragraph("<b>RECIBO DE PAGAMENTO</b>", title_style))
    elements.append(Paragraph(f"<b>Recibo Nº:</b> {receipt_data['ID']}", normal_style))
    elements.append(Paragraph(f"<b>Data:</b> {receipt_data['Data']}", normal_style))
    elements.append(Spacer(1, 10))
    
    elements.append(Paragraph(f"Recebemos de: <b>{receipt_data['Cliente']}</b>", normal_style))
    elements.append(Paragraph(f"A quantia de: <b>R$ {receipt_data['Total']:.2f}</b>", normal_style))
    elements.append(Spacer(1, 10))
    
    elements.append(Paragraph("<b>Referente ao produto/serviço:</b>", normal_style))
    elements.append(Paragraph(f"- Produto: {receipt_data['Produto']} (Qtd: {receipt_data['Quantidade']}x R$ {receipt_data['Valor Unitário']:.2f})", normal_style))
    elements.append(Spacer(1, 40))
    
    elements.append(Paragraph("___________________________________________________", ParagraphStyle('Sign', alignment=1, parent=normal_style)))
    elements.append(Paragraph("Assinatura / Carimbo", ParagraphStyle('SignLabel', alignment=1, parent=normal_style)))
    
    doc.build(elements)
    return pdf_path

# Interface Principal
st.title("🧾 Sistema de Recibos e Gestão de Vendas")

menu = st.sidebar.selectbox("Navegação", ["Registrar Venda / Emitir Recibo", "Indicadores e Relatórios"])

if menu == "Registrar Venda / Emitir Recibo":
    st.header("Novo Lançamento de Venda")
    
    with st.form("form_venda"):
        col1, col2 = st.columns(2)
        with col1:
            cliente = st.text_input("Nome do Cliente")
            produto = st.text_input("Nome do Produto / Serviço")
        with col2:
            quantidade = st.number_input("Quantidade", min_value=1, value=1, step=1)
            valor_unitario = st.number_input("Valor Unitário (R$)", min_value=0.0, value=0.0, format="%.2f")
            
        data_venda = st.date_input("Data da Venda", value=datetime.today())
        
        submitted = st.form_submit_button("Salvar Venda e Gerar Recibo")
        
        if submitted:
            if cliente and produto and valor_unitario > 0:
                total = quantidade * valor_unitario
                sale_id = len(st.session_state.sales_data) + 1
                
                new_row = {
                    "ID": sale_id,
                    "Data": data_venda.strftime('%Y-%m-%d'),
                    "Cliente": cliente,
                    "Produto": produto,
                    "Quantidade": quantidade,
                    "Valor Unitário": valor_unitario,
                    "Total": total
                }
                
                st.session_state.sales_data = pd.concat([
                    st.session_state.sales_data, 
                    pd.DataFrame([new_row])
                ], ignore_index=True)
                
                st.success("Venda registrada com sucesso!")
                
                # Gerar PDF do Recibo Individual
                pdf_file = generate_receipt_pdf(new_row)
                with open(pdf_file, "rb") as f:
                    st.download_button(
                        label="📥 Baixar Recibo em PDF",
                        data=f,
                        file_name=f"recibo_{sale_id}.pdf",
                        mime="application/pdf"
                    )
            else:
                st.error("Por favor, preencha todos os campos obrigatórios corretamente.")

elif menu == "Indicadores e Relatórios":
    st.header("📊 Indicadores de Entrada e Relatórios por Período")
    
    if st.session_state.sales_data.empty:
        st.info("Nenhuma venda registrada até o momento.")
    else:
        # Filtros de Período
        st.sidebar.subheader("Filtro de Período")
        
        # Converter coluna Data para datetime para filtragem
        df_display = st.session_state.sales_data.copy()
        df_display["Data_dt"] = pd.to_datetime(df_display["Data"])
        
        min_date = df_display["Data_dt"].min().date()
        max_date = df_display["Data_dt"].max().date()
        
        start_date = st.sidebar.date_input("Data Inicial", value=min_date, min_value=min_date, max_value=max_date)
        end_date = st.sidebar.date_input("Data Final", value=max_date, min_value=min_date, max_value=max_date)
        
        # Aplicar filtro
        mask = (df_display["Data_dt"].dt.date >= start_date) & (df_display["Data_dt"].dt.date <= end_date)
        df_filtered = df_display.loc[mask].copy()
        
        # Métricas / Indicadores de Entrada
        col1, col2, col3 = st.columns(3)
        total_faturamento = df_filtered["Total"].sum()
        total_produtos_vendidos = df_filtered["Quantidade"].sum()
        total_transacoes = len(df_filtered)
        
        col1.metric("Faturamento no Período", f"R$ {total_faturamento:.2f}")
        col2.metric("Total de Itens Vendidos", int(total_produtos_vendidos))
        col3.metric("Qtd. de Vendas", total_transacoes)
        
        st.markdown("---")
        st.subheader("Lista de Vendas Filtradas")
        st.dataframe(df_filtered.drop(columns=["Data_dt"]), use_container_width=True)
        
        # Geração do Relatório PDF Filtrado
        st.markdown("### Exportar Relatório")
        if not df_filtered.empty:
            if st.button("Gerar Relatório em PDF"):
                pdf_rel_path = generate_sales_report_pdf(df_filtered, start_date, end_date)
                with open(pdf_rel_path, "rb") as f:
                    st.download_button(
                        label="📥 Baixar Relatório em PDF",
                        data=f,
                        file_name="relatorio_vendas_periodo.pdf",
                        mime="application/pdf"
                    )
        else:
            st.warning("Não há dados no período selecionado para gerar o relatório.")

