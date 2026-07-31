ATUALIZAR OS SEGUINTES ITENS:

COPIEI O ARQUIVO setup_wizard.js para PT-BR

411				default: "Português Brasileiro",

ATUALIZADO O ARQUIVO setup_wizard.PY FUNÇÃO def load_languages():

@frappe.whitelist()
def load_languages():
	Language = frappe.qb.DocType("Language")
	allowed_codes = ["pt-BR", "en", "es"]
	priority = {"pt-BR": 0, "en": 1, "es": 2}

	language_codes = (
		frappe.qb.from_(Language)
		.select(Language.language_code, Language.language_name)
		.where(Language.enabled == 1)
		.where(Language.language_code.isin(allowed_codes))
		.run(as_dict=1)
	)

	language_opts = (
		frappe.qb.from_(Language)
		.select(
			Language.language_name.as_("value"),
			Language.language_name.as_("label"),
			Language.language_code.as_("description"),
		)
		.where(Language.enabled == 1)
		.where(Language.language_code.isin(allowed_codes))
		.run(as_dict=1)
	)

	language_codes = sorted(
		language_codes, key=lambda d: priority.get(d["language_code"], 99)
	)
	language_opts = sorted(
		language_opts, key=lambda d: priority.get(d["description"], 99)
	)

	codes_to_names = {}
	for d in language_codes:
		codes_to_names[d.language_code] = d.language_name

	default_language_name = frappe.db.get_value("Language", frappe.local.lang, "language_name")
	if not default_language_name:
		default_language_name = "Português Brasileiro"

	return {
		"default_language": default_language_name,
		"languages": language_opts,
		"codes_to_names": codes_to_names,
	}


Atualizado em public/imagens em ambos apps icones para erpz 

Atualizado erpnext_settings.json; main.pot; erpnext_settings.json; de ERPNext Settings para ERPZ Settings

Atualizado system_settings.json;  de Frappe  para ERPZ 

atualizado arquivo desktop.js 462 para window.open("https://suporte.erpz.io/help", "_blank"); e traduzido o arquivo.


Ajustado about.js:

	$(dialog.body).html(
			<div class="about-frappe-section">
				<p class="about-tagline">Consultoria e desenvolvimento para suas rotinas aqui:</p>
				<p><strong>Site:</strong> <a href="https://erpz.io" target="_blank">erpz.io</a></p>

				<p class="about-tagline">Desenvolvimentos:</p>
				<p><strong>Site:</strong> <a href="https://andradez.dev" target="_blank">andradez.dev</a></p>

				<p class="about-tagline">Busque consultores aqui:</p>
				<p><strong>Site:</strong> <a href="https://consultorez.app" target="_blank">consultorez.app</a></p>

				<p class="about-tagline">Consultoria de automacao industrial e ERP aqui:</p>
				<p><strong>Site:</strong> <a href="https://industriaz.io" target="_blank">industriaz.io</a></p>

				<p class="about-tagline">Chat IA para seu atendimento aos clientes:</p>
				<p><strong>Site:</strong> <a href="https://denizi.io" target="_blank">denizi.io</a></p>

				<p class="about-tagline">Precisa de suporte, acione agora:</p>
				<p><strong>Site:</strong> <a href="https://suporte.erpz.io" target="_blank">suporte.erpz.io</a></p>
			</div>
	);


    ATUALIZADO pt-BR.po e en.po palavra Frappe para ERPZ

atuaizado {{ _("Built on {0}").format('<a href="https://frappeframework.com?source=website_footer" target="_blank" class="text-muted">Frappe</a>') }}

para 

{{ _("Built on {0}").format('<a href="https://erpz.io" target="_blank" class="text-muted">ERPZ</a>') }}

ATUALIZADO login.html para ERPZ
	<h4>{{ _('Login to {0}').format(app_name or _("ERPZ")) }}</h4>



TRADUZIDO ARQUIVO COMPLETO login.html 


