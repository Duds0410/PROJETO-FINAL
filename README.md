import flet as ft

def main(page: ft.Page):
    page.title = 'Authenticator'
    page.horizontal_alignment = ft.CrossAxisAlignment.CENTER
    page.vertical_alignment = ft.MainAxisAlignment.CENTER
    page.window.resizable = False
    page.window.maximized = True
    page.padding = ft.padding.all(0)
    page.bgcolor = ft.colors.PURPLE_800

    # Lista para armazenar as notas publicadas
    notas_publicadas = []

    # Referência para o campo de texto onde o usuário vai digitar a nota
    nota_textfield = ft.Ref()

    def logar(e: ft.ControlEvent):
        page.controls.clear()  # Limpa todas as telas
        page.add(tela_publicacao)  # Exibe a tela de publicação de notas

    def publicar_nota(e: ft.ControlEvent):
        texto_nota = nota_textfield.current.value
        if texto_nota:
            notas_publicadas.append(texto_nota)
            nota_textfield.current.value = ""  # Limpa o campo de texto
            exibir_notas()

    def exibir_notas():
        lista_notas = ft.Column(
            controls=[ft.Text(value=nota, color=ft.colors.WHITE, size=14) for nota in notas_publicadas],
            scroll=ft.ScrollMode.AUTO
        )
        # Atualiza a lista de notas na tela de publicação
        tela_publicacao.controls[-1] = lista_notas
        page.update()

    def voltar_login(e: ft.ControlEvent):
        page.controls.clear()
        page.add(login)  # Exibe a tela de login novamente

    def exibir_tela_cadastro(e: ft.ControlEvent):
        page.controls.clear()
        page.add(tela_cadastro)

    def exibir_tela_recuperar_senha(e: ft.ControlEvent):
        page.controls.clear()
        page.add(tela_recuperar_senha)

    # Tela de Cadastro
    tela_cadastro = ft.Column(
        controls=[
            ft.Container(
                bgcolor=ft.colors.BLACK,
                border_radius=10,
                width=400,
                padding=ft.padding.all(10),
                content=ft.Column(
                    controls=[
                        ft.Row(
                            controls=[
                                ft.IconButton(
                                    icon=ft.icons.ARROW_BACK,
                                    on_click=voltar_login,
                                    icon_size=30,
                                    bgcolor=ft.colors.PURPLE_600,
                                    icon_color=ft.colors.WHITE
                                )
                            ],
                            alignment=ft.MainAxisAlignment.START
                        ),
                        ft.Text(
                            value='Criar Nova Conta',
                            weight='bold',
                            size=20,
                            color=ft.colors.WHITE
                        ),
                        ft.Divider(color=ft.colors.PURPLE, thickness=1),
                        ft.TextField(hint_text="Digite seu email", prefix_icon=ft.icons.EMAIL),
                        ft.TextField(hint_text="Digite sua senha", prefix_icon=ft.icons.LOCK, password=True),
                        ft.TextField(hint_text="Confirme sua senha", prefix_icon=ft.icons.LOCK, password=True),
                        ft.ElevatedButton(
                            text="Cadastrar",
                            color=ft.colors.WHITE,
                            bgcolor=ft.colors.PURPLE
                        )
                    ],
                    spacing=10,
                    horizontal_alignment=ft.CrossAxisAlignment.CENTER
                )
            )
        ],
        alignment=ft.MainAxisAlignment.CENTER,
        horizontal_alignment=ft.CrossAxisAlignment.CENTER
    )

    # Tela de Recuperação de Senha
    tela_recuperar_senha = ft.Column(
        controls=[
            ft.Container(
                bgcolor=ft.colors.BLACK,
                border_radius=10,
                width=400,
                padding=ft.padding.all(10),
                content=ft.Column(
                    controls=[
                        ft.Row(
                            controls=[
                                ft.IconButton(
                                    icon=ft.icons.ARROW_BACK,
                                    on_click=voltar_login,
                                    icon_size=30,
                                    bgcolor=ft.colors.PURPLE_600,
                                    icon_color=ft.colors.WHITE
                                )
                            ],
                            alignment=ft.MainAxisAlignment.START
                        ),
                        ft.Text(
                            value='Recuperar Senha',
                            weight='bold',
                            size=20,
                            color=ft.colors.WHITE
                        ),
                        ft.Divider(color=ft.colors.PURPLE, thickness=1),
                        ft.TextField(hint_text="Digite seu email", prefix_icon=ft.icons.EMAIL),
                        ft.ElevatedButton(
                            text="Enviar Instruções",
                            color=ft.colors.WHITE,
                            bgcolor=ft.colors.PURPLE
                        )
                    ],
                    spacing=10,
                    horizontal_alignment=ft.CrossAxisAlignment.CENTER
                )
            )
        ],
        alignment=ft.MainAxisAlignment.CENTER,
        horizontal_alignment=ft.CrossAxisAlignment.CENTER
    )

    # Tela de Publicação de Nota
    tela_publicacao = ft.Column(
        controls=[
            ft.Container(
                bgcolor=ft.colors.BLACK,
                border_radius=10,
                width=400,
                padding=ft.padding.all(10),
                content=ft.Column(
                    controls=[
                        ft.Row(
                            controls=[
                                ft.IconButton(
                                    icon=ft.icons.ARROW_BACK,
                                    on_click=voltar_login,
                                    icon_size=30,
                                    bgcolor=ft.colors.PURPLE_600,
                                    icon_color=ft.colors.WHITE
                                )
                            ],
                            alignment=ft.MainAxisAlignment.START
                        ),
                        ft.Text(
                            value='Publicar uma Nota',
                            weight='bold',
                            size=20,
                            color=ft.colors.WHITE
                        ),
                        ft.Divider(color=ft.colors.PURPLE, thickness=1),
                        ft.TextField(
                            hint_text='Digite sua nota aqui...',
                            ref=nota_textfield
                        ),
                        ft.ElevatedButton(
                            text='Publicar Nota',
                            color=ft.colors.WHITE,
                            bgcolor=ft.colors.PURPLE,
                            on_click=publicar_nota
                        ),
                        ft.Column(
                            controls=[
                                ft.Text(value=nota, color=ft.colors.WHITE, size=14)
                                for nota in notas_publicadas
                            ],
                            scroll=ft.ScrollMode.AUTO
                        )
                    ],
                    spacing=10,
                    horizontal_alignment=ft.CrossAxisAlignment.CENTER
                )
            )
        ],
        alignment=ft.MainAxisAlignment.CENTER,
        horizontal_alignment=ft.CrossAxisAlignment.CENTER
    )

    # Tela de Login
    login = ft.Column(
        controls=[
            ft.Container(
                bgcolor=ft.colors.BLACK,
                border_radius=10,
                width=400,
                height=320,
                padding=ft.padding.all(10),
                content=ft.Column(
                    controls=[
                        ft.Text(
                            value='Sign-In',
                            weight='bold',
                            size=20,
                            color=ft.colors.WHITE
                        ),
                        ft.Divider(color=ft.colors.PURPLE, thickness=1),
                        ft.TextField(hint_text='Digite seu email', prefix_icon=ft.icons.PERSON),
                        ft.TextField(hint_text='Digite sua senha', prefix_icon=ft.icons.LOCK, password=True),
                        ft.ElevatedButton(
                            text='Sign-In',
                            color=ft.colors.WHITE,
                            bgcolor=ft.colors.PURPLE,
                            on_click=logar
                        ),
                        ft.Row(
                            controls=[
                                ft.TextButton(
                                    text='Recuperar senha',
                                    on_click=exibir_tela_recuperar_senha
                                ),
                                ft.TextButton(
                                    text='Criar nova conta',
                                    on_click=exibir_tela_cadastro
                                )
                            ],
                            alignment=ft.MainAxisAlignment.SPACE_BETWEEN
                        )
                    ],
                    spacing=10,
                    horizontal_alignment=ft.CrossAxisAlignment.CENTER
                )
            )
        ],
        alignment=ft.MainAxisAlignment.CENTER,
        horizontal_alignment=ft.CrossAxisAlignment.CENTER
    )

    # Exibe a tela de login inicialmente
    page.add(login)

if __name__ == '__main__':
    ft.app(target=main)
