from flask import Flask, render_template, request

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('formulario.html')

@app.route('/processar_respostas', methods=['POST'])
def processar_respostas():
    # Recebendo as respostas do formulário
    data = request.form['data']
    terapeuta = request.form['terapeuta']
    nome_crianca = request.form['nome_crianca']
    estado_crianca = request.form['estado_crianca']
    recursos_utilizados = request.form['recursos_utilizados']
    objetivos_sessao = request.form['objetivos_sessao']
    dificuldade_descricao = request.form['dificuldade_descricao']
    facilidade_descricao = request.form['facilidade_descricao']
    atingiu_objetivos = request.form['atingiu_objetivos']
    proxima_sessao = request.form['proxima_sessao']
    encaminhamento = request.form['encaminhamento']

    # Modelo do relatório
    modelo = """
    No dia {data} iniciamos a terapia com a presença da {terapeuta}.
    {nome_crianca} chegou em sala {estado_crianca}.
    Os recursos utilizados foram {recursos_utilizados}.
    Os objetivos trabalhados na sessão foram {objetivos_sessao}.
    {nome_crianca} apresentou {dificuldade_descricao}.
    {facilidade_descricao}.
    Atingiu os objetivos propostos da sessão: {atingiu_objetivos}.
    Na próxima sessão será trabalhado {proxima_sessao}.
    A criança foi encaminhada {encaminhamento}.
    """

    # Substituindo as variáveis no modelo
    relatorio_preenchido = modelo.format(
        data=data,
        terapeuta=terapeuta,
        nome_crianca=nome_crianca,
        estado_crianca=estado_crianca,
        recursos_utilizados=recursos_utilizados,
        objetivos_sessao=objetivos_sessao,
        dificuldade_descricao=dificuldade_descricao,
        facilidade_descricao=facilidade_descricao,
        atingiu_objetivos=atingiu_objetivos,
        proxima_sessao=proxima_sessao,
        encaminhamento=encaminhamento
    )

    # Exibindo o relatório preenchido
    return relatorio_preenchido

if __name__ == '__main__':
    app.run(debug=True)
