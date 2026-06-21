# CLAUDE.md — Mazo de Repetición Espaciada IELTS (Vocabulario + Gramática)

Datos de tarjetas para una app de estudio espaciado (estilo AnkiDroid).
Usuario: Juan · Lengua materna: español · Objetivo: IELTS Academic, Band 5.5 → 7+.
Todo el contenido proviene de la guía de estudio de vocabulario y gramática.

---

## Propósito del archivo
Este archivo es la **fuente de datos de las tarjetas**. El contenido está en campos atómicos (no en prosa) para que la app pueda construir tarjetas en cualquier dirección y de varios tipos.

## Esquema de datos (cómo parsear cada mazo)
- **Vocabulario / Colocaciones / Tendencias:** campos `en` (inglés), `es` (español), `example` (ejemplo en inglés), `topic` (etiqueta).
  - Genera DOS tarjetas por fila: `en → es` (reconocimiento, ayuda a Reading/Listening) y `es → en` (producción, ayuda a Writing/Speaking). La producción es la más valiosa para subir de banda.
- **Upgrades:** campos `basic`, `upgrades`, `note`. Tarjeta: front = `basic`, back = `upgrades` + `note`.
- **Gramática (conceptos):** campos `concept`, `rule_es`, `example_en`, `tag`. Tarjeta: front = `concept`, back = `rule_es` + `example_en`. Alternativa recomendada: convertir `example_en` en tarjeta **cloze** ocultando el elemento gramatical clave.
- **Errores (corrección):** campos `wrong`, `right`, `why_es`. Tarjeta: front = "Corrige: {wrong}", back = `{right}` + `{why_es}`. Estas son las de mayor valor para ti como hispanohablante.

## Diseño de repetición espaciada (notas para la app)
1. **Tarjetas bidireccionales** para vocabulario; prioriza la dirección `es → en` en la cola de repaso (recuerdo activo > reconocimiento).
2. **Cloze para gramática:** ocultar la forma verbal/artículo/preposición fuerza el recuerdo activo de la regla, no solo reconocerla.
3. **Prioridad inicial (primeras 2 semanas):** mazo `errores-hispanohablante` + gramática de `present-perfect`, `articulos`, `concordancia`, `preposiciones`, `oraciones-complejas`. Son tus fugas de puntos más probables.
4. **Una colocación cuenta como una unidad** (`conduct research`), nunca tarjetas de palabras sueltas.
5. **Tags** = `topic`/`tag` de cada fila, para filtrar mazos y medir progreso por área.
6. **Intervalos:** algoritmo SR estándar (SM-2 o similar). Tarjeta fallada → vuelve a intervalo corto; acertada → intervalo crece.

---

# MAZO 1 — VOCABULARIO POR TEMA

## 1.1 Education
| en | es | example | topic |
|---|---|---|---|
| curriculum | plan de estudios | The school revised its curriculum. | education |
| tuition fees | matrícula / tasas académicas | Rising tuition fees deter many students. | education |
| lifelong learning | aprendizaje permanente | Lifelong learning is essential today. | education |
| academic achievement | logro / rendimiento académico | Her academic achievement was outstanding. | education |
| distance learning | educación a distancia | Distance learning expanded during the pandemic. | education |
| higher education | educación superior | Higher education has become more accessible. | education |
| literacy rate | tasa de alfabetización | The literacy rate has risen sharply. | education |
| vocational training | formación profesional | Vocational training prepares students for trades. | education |
| rote learning | aprendizaje memorístico | Rote learning discourages critical thinking. | education |
| critical thinking | pensamiento crítico | Schools should foster critical thinking. | education |
| to acquire knowledge | adquirir conocimientos | Students acquire knowledge through practice. | education |
| to broaden one's horizons | ampliar horizontes | Travel broadens one's horizons. | education |
| a well-rounded education | una educación integral | A well-rounded education develops many skills. | education |
| scholarship | beca | She won a scholarship to study abroad. | education |
| dropout rate | tasa de abandono escolar | The dropout rate remains a concern. | education |

## 1.2 Environment
| en | es | example | topic |
|---|---|---|---|
| climate change | cambio climático | Governments must act to combat climate change. | environment |
| global warming | calentamiento global | Global warming threatens coastal cities. | environment |
| carbon footprint | huella de carbono | Reducing our carbon footprint requires action. | environment |
| greenhouse gas emissions | emisiones de gases de efecto invernadero | Greenhouse gas emissions continue to rise. | environment |
| renewable energy | energía renovable | Renewable energy is becoming cheaper. | environment |
| fossil fuels | combustibles fósiles | We must reduce our reliance on fossil fuels. | environment |
| sustainability | sostenibilidad | Sustainability should guide development. | environment |
| environmental degradation | degradación ambiental | Environmental degradation harms wildlife. | environment |
| deforestation | deforestación | Deforestation accelerates climate change. | environment |
| biodiversity | biodiversidad | Deforestation reduces biodiversity. | environment |
| to deplete natural resources | agotar recursos naturales | Overconsumption depletes natural resources. | environment |
| to mitigate the effects of | mitigar los efectos de | Policies aim to mitigate the effects of pollution. | environment |
| conservation | conservación | Conservation protects endangered species. | environment |
| pollution | contaminación | Air pollution affects public health. | environment |
| ecosystem | ecosistema | Pollution disrupts the ecosystem. | environment |

## 1.3 Technology
| en | es | example | topic |
|---|---|---|---|
| artificial intelligence | inteligencia artificial | Artificial intelligence is transforming industries. | technology |
| automation | automatización | Automation has boosted productivity but cut jobs. | technology |
| digital divide | brecha digital | The digital divide limits opportunities. | technology |
| cybersecurity | ciberseguridad | Cybersecurity is a growing priority. | technology |
| innovation | innovación | Innovation drives economic growth. | technology |
| cloud computing | computación en la nube | Cloud computing reduces costs for firms. | technology |
| virtual reality | realidad virtual | Virtual reality is used in training. | technology |
| data privacy | privacidad de datos | Data privacy concerns are increasing. | technology |
| to revolutionise | revolucionar | Smartphones revolutionised communication. | technology |
| cutting-edge technology | tecnología de vanguardia | The lab uses cutting-edge technology. | technology |
| social media platform | plataforma de redes sociales | Social media platforms shape opinions. | technology |
| to pose a risk to | suponer un riesgo para | Excessive screen time poses a risk to health. | technology |
| screen time | tiempo frente a pantallas | Children's screen time has increased. | technology |
| tech-savvy | experto en tecnología | Younger users tend to be tech-savvy. | technology |
| to streamline | agilizar / optimizar | Software streamlines the workflow. | technology |

## 1.4 Health
| en | es | example | topic |
|---|---|---|---|
| public health | salud pública | Vaccination improves public health. | health |
| a balanced diet | una dieta equilibrada | A balanced diet prevents many illnesses. | health |
| sedentary lifestyle | estilo de vida sedentario | A sedentary lifestyle increases health risks. | health |
| mental health | salud mental | Mental health deserves more attention. | health |
| preventive measures | medidas preventivas | Preventive measures reduce disease. | health |
| obesity | obesidad | Obesity rates have risen in many countries. | health |
| healthcare system | sistema sanitario | The healthcare system is under strain. | health |
| chronic illness | enfermedad crónica | Chronic illness affects quality of life. | health |
| well-being | bienestar | Exercise improves overall well-being. | health |
| to raise awareness of | concienciar sobre | Campaigns raise awareness of mental health. | health |
| life expectancy | esperanza de vida | Life expectancy has increased globally. | health |
| to alleviate symptoms | aliviar síntomas | The treatment alleviates symptoms quickly. | health |
| immune system | sistema inmunitario | Sleep strengthens the immune system. | health |
| stress-related | relacionado con el estrés | Stress-related illness is common at work. | health |
| to contribute to | contribuir a | Poor diet contributes to obesity. | health |

## 1.5 Work
| en | es | example | topic |
|---|---|---|---|
| unemployment rate | tasa de desempleo | The unemployment rate fell last year. | work |
| job satisfaction | satisfacción laboral | Job satisfaction boosts productivity. | work |
| work-life balance | equilibrio trabajo-vida | Remote work can improve work-life balance. | work |
| remote working | teletrabajo | Remote working has become widespread. | work |
| the labour market | el mercado laboral | The labour market is highly competitive. | work |
| career prospects | perspectivas profesionales | A degree improves career prospects. | work |
| to pursue a career | seguir una carrera profesional | She decided to pursue a career in law. | work |
| wages | salario | Wages have stagnated for years. | work |
| job security | estabilidad laboral | Many workers value job security. | work |
| productivity | productividad | Automation raises productivity. | work |
| skilled labour | mano de obra cualificada | The sector needs skilled labour. | work |
| to make redundant | despedir por reducción | Hundreds were made redundant. | work |
| a demanding job | un trabajo exigente | Nursing is a demanding job. | work |
| professional development | desarrollo profesional | The firm funds professional development. | work |
| the gig economy | economía de trabajos esporádicos | The gig economy offers flexibility but little security. | work |

## 1.6 Society and family
| en | es | example | topic |
|---|---|---|---|
| nuclear family | familia nuclear | The nuclear family is becoming smaller. | society |
| extended family | familia extensa | Extended families often live together. | society |
| upbringing | crianza | A stable upbringing benefits children. | society |
| ageing population | envejecimiento de la población | An ageing population strains pensions. | society |
| social cohesion | cohesión social | Diversity can strengthen social cohesion. | society |
| gender equality | igualdad de género | Gender equality has improved gradually. | society |
| generation gap | brecha generacional | Technology widens the generation gap. | society |
| peer pressure | presión de grupo | Peer pressure influences teenagers. | society |
| to bring up children | criar hijos | It is hard to bring up children alone. | society |
| single-parent family | familia monoparental | Single-parent families face challenges. | society |
| social mobility | movilidad social | Education promotes social mobility. | society |
| multiculturalism | multiculturalismo | Multiculturalism enriches society. | society |
| to foster | fomentar / cultivar | Schools foster a sense of community. | society |
| marginalised groups | grupos marginados | Policies should protect marginalised groups. | society |
| welfare | bienestar / asistencia social | Welfare supports vulnerable families. | society |

## 1.7 Crime and justice
| en | es | example | topic |
|---|---|---|---|
| to commit a crime | cometer un delito | Few people commit serious crimes. | crime |
| offender | delincuente / infractor | Young offenders need rehabilitation. | crime |
| crime rate | tasa de criminalidad | The crime rate has fallen recently. | crime |
| deterrent | elemento disuasorio | Tougher sentences may act as a deterrent. | crime |
| rehabilitation | reinserción / rehabilitación | Rehabilitation reduces reoffending. | crime |
| to reoffend | reincidir | Many former inmates reoffend. | crime |
| recidivism | reincidencia | Education programmes lower recidivism. | crime |
| prison sentence | pena de prisión | He received a long prison sentence. | crime |
| incarceration | encarcelamiento | Incarceration is costly for society. | crime |
| probation | libertad condicional / vigilada | She was released on probation. | crime |
| legislation | legislación | New legislation targets cybercrime. | crime |
| law enforcement | fuerzas del orden | Law enforcement needs more resources. | crime |
| juvenile delinquency | delincuencia juvenil | Poverty fuels juvenile delinquency. | crime |
| to impose a penalty | imponer una sanción | Courts can impose a heavy penalty. | crime |
| white-collar crime | delito de cuello blanco | White-collar crime often goes unpunished. | crime |

## 1.8 Government, politics and economy
| en | es | example | topic |
|---|---|---|---|
| to implement a policy | aplicar una política | The government implemented a new policy. | politics |
| democracy | democracia | Democracy depends on participation. | politics |
| to pass a law | aprobar una ley | Parliament passed the law last month. | politics |
| public sector | sector público | The public sector employs millions. | politics |
| taxation | fiscalidad / impuestos | Higher taxation funds public services. | politics |
| economic growth | crecimiento económico | Economic growth slowed this year. | politics |
| recession | recesión | The economy entered a recession. | politics |
| inflation | inflación | Inflation eroded household incomes. | politics |
| subsidy | subvención | Farmers receive a government subsidy. | politics |
| infrastructure | infraestructura | Investment in infrastructure boosts growth. | politics |
| welfare state | estado del bienestar | The welfare state supports the unemployed. | politics |
| gross domestic product | producto interior bruto | GDP measures economic output. | politics |
| accountability | rendición de cuentas | Voters demand greater accountability. | politics |
| to allocate funds | asignar fondos | The council allocated funds to housing. | politics |
| regulation | regulación / normativa | Stricter regulation protects consumers. | politics |

## 1.9 Media and advertising
| en | es | example | topic |
|---|---|---|---|
| mass media | medios de masas | Mass media shape public opinion. | media |
| advertising campaign | campaña publicitaria | The advertising campaign was a success. | media |
| bias | sesgo | News coverage can show political bias. | media |
| censorship | censura | Censorship limits freedom of expression. | media |
| propaganda | propaganda | Propaganda distorts the truth. | media |
| misinformation | desinformación | Misinformation spreads quickly online. | media |
| clickbait | cebo de clics | Clickbait headlines mislead readers. | media |
| sensationalism | sensacionalismo | Sensationalism sells newspapers. | media |
| freedom of the press | libertad de prensa | Freedom of the press is vital. | media |
| to manipulate public opinion | manipular la opinión pública | Adverts can manipulate public opinion. | media |
| target audience | público objetivo | The ad reached its target audience. | media |
| consumerism | consumismo | Advertising fuels consumerism. | media |
| influencer | influencer | Influencers shape buying habits. | media |
| media literacy | alfabetización mediática | Media literacy helps spot fake news. | media |
| to shape attitudes | moldear actitudes | The media shapes public attitudes. | media |

## 1.10 Travel and tourism
| en | es | example | topic |
|---|---|---|---|
| public transport | transporte público | Public transport reduces congestion. | travel |
| traffic congestion | congestión del tráfico | Traffic congestion wastes time and fuel. | travel |
| tourism industry | industria turística | The tourism industry supports local jobs. | travel |
| sustainable tourism | turismo sostenible | Sustainable tourism protects the environment. | travel |
| ecotourism | ecoturismo | Ecotourism is growing in popularity. | travel |
| off the beaten track | fuera de las rutas turísticas | They prefer places off the beaten track. | travel |
| itinerary | itinerario | We planned a detailed itinerary. | travel |
| accommodation | alojamiento | Accommodation can be expensive in peak season. | travel |
| a breathtaking view | una vista impresionante | The summit offers a breathtaking view. | travel |
| cultural exchange | intercambio cultural | Travel encourages cultural exchange. | travel |
| mass tourism | turismo masivo | Mass tourism damages fragile sites. | travel |
| peak season | temporada alta | Prices rise in peak season. | travel |
| to commute | desplazarse al trabajo | Many people commute by train. | travel |
| commercialisation | comercialización | Commercialisation has changed the festival. | travel |
| infrastructure | infraestructura | Tourism requires good infrastructure. | travel |

## 1.11 Globalization and culture
| en | es | example | topic |
|---|---|---|---|
| globalisation | globalización | Globalisation connects economies. | globalization |
| multinational corporation | multinacional | Multinational corporations dominate trade. | globalization |
| cultural identity | identidad cultural | Globalisation can erode cultural identity. | globalization |
| cultural homogenisation | homogeneización cultural | Cultural homogenisation reduces diversity. | globalization |
| outsourcing | externalización | Outsourcing lowers production costs. | globalization |
| interdependence | interdependencia | Trade creates global interdependence. | globalization |
| brain drain | fuga de cerebros | Brain drain harms developing nations. | globalization |
| free trade | libre comercio | Free trade boosts economic growth. | globalization |
| cultural heritage | patrimonio cultural | Tourism can threaten cultural heritage. | globalization |
| to preserve traditions | preservar tradiciones | Communities strive to preserve traditions. | globalization |
| assimilation | asimilación cultural | Assimilation can weaken minority cultures. | globalization |
| diaspora | diáspora | The diaspora maintains its customs abroad. | globalization |
| economic integration | integración económica | Economic integration benefits members. | globalization |
| a global village | una aldea global | Technology has created a global village. | globalization |
| to erode | erosionar / debilitar | Globalisation can erode local values. | globalization |

## 1.12 Urbanization and housing
| en | es | example | topic |
|---|---|---|---|
| urbanisation | urbanización | Rapid urbanisation strains services. | urbanization |
| overpopulation | superpoblación | Overpopulation worsens housing shortages. | urbanization |
| urban sprawl | expansión urbana descontrolada | Urban sprawl consumes farmland. | urbanization |
| affordable housing | vivienda asequible | Cities need more affordable housing. | urbanization |
| slum | barrio marginal / chabolas | Slums lack basic sanitation. | urbanization |
| gentrification | gentrificación | Gentrification displaces poorer residents. | urbanization |
| rural-to-urban migration | migración del campo a la ciudad | Rural-to-urban migration is accelerating. | urbanization |
| high-rise buildings | edificios de gran altura | High-rise buildings save space. | urbanization |
| green spaces | zonas verdes | Green spaces improve well-being. | urbanization |
| cost of living | coste de vida | The cost of living keeps rising. | urbanization |
| public amenities | servicios públicos | Good public amenities attract residents. | urbanization |
| congestion | congestión | Congestion is a major urban problem. | urbanization |
| a smart city | una ciudad inteligente | A smart city uses data to manage traffic. | urbanization |
| standard of living | nivel de vida | Cities often offer a higher standard of living. | urbanization |
| infrastructure | infraestructura | Urban growth demands new infrastructure. | urbanization |

## 1.13 Art and entertainment
| en | es | example | topic |
|---|---|---|---|
| cultural heritage | patrimonio cultural | Museums preserve cultural heritage. | art |
| to express creativity | expresar la creatividad | Art allows people to express creativity. | art |
| performing arts | artes escénicas | The performing arts enrich communities. | art |
| exhibition | exposición | The exhibition attracted many visitors. | art |
| mainstream | comercial / mayoritario | The band moved into the mainstream. | art |
| niche | minoritario / nicho | The gallery serves a niche audience. | art |
| to fund the arts | financiar las artes | Governments should fund the arts. | art |
| aesthetic value | valor estético | The building has great aesthetic value. | art |
| masterpiece | obra maestra | The painting is considered a masterpiece. | art |
| to broaden cultural understanding | ampliar la comprensión cultural | Travel broadens cultural understanding. | art |
| leisure activities | actividades de ocio | Leisure activities reduce stress. | art |
| the entertainment industry | la industria del entretenimiento | The entertainment industry is booming. | art |
| patronage | mecenazgo | Royal patronage funded great art. | art |
| thought-provoking | que invita a la reflexión | The film was thought-provoking. | art |
| to enrich society | enriquecer la sociedad | The arts enrich society. | art |

---

# MAZO 2 — FRASES ACADÉMICAS (opinión, acuerdo, conectores)

## 2.1 Opinion
| en | es | example | topic |
|---|---|---|---|
| In my view | En mi opinión | In my view, this policy is flawed. | opinion |
| From my perspective | Desde mi punto de vista | From my perspective, education is key. | opinion |
| I am convinced that | Estoy convencido de que | I am convinced that change is needed. | opinion |
| It is my firm belief that | Tengo la firme convicción de que | It is my firm belief that taxes should rise. | opinion |
| It seems to me that | Me parece que | It seems to me that the benefits outweigh the costs. | opinion |
| I would argue that | Yo sostengo que | I would argue that funding should increase. | opinion |
| It is undeniable that | No cabe duda de que | It is undeniable that technology has transformed work. | opinion |
| As far as I am concerned | En lo que a mí respecta | As far as I am concerned, the plan is sensible. | opinion |

## 2.2 Agree / disagree
| en | es | example | topic |
|---|---|---|---|
| I completely agree that | Estoy totalmente de acuerdo en que | I completely agree that reading is vital. | agreement |
| I partially agree that | Estoy parcialmente de acuerdo en que | I partially agree that fines reduce crime. | agreement |
| While I accept that, I believe | Aunque admito que, creo que | While I accept that cars are useful, I believe they pollute. | agreement |
| I am inclined to disagree | Me inclino a estar en desacuerdo | I am inclined to disagree with this claim. | agreement |
| I take the opposite view | Sostengo la postura contraria | On this issue I take the opposite view. | agreement |
| It is often argued that, however | Se suele argumentar que, sin embargo | It is often argued that money brings happiness; however, evidence is mixed. | agreement |

## 2.3 Connectors (cohesion)
| en | es | example | topic |
|---|---|---|---|
| due to | debido a (+ sustantivo) | Sales fell due to the recession. | connector-cause |
| as a result | como resultado | Demand rose; as a result, prices increased. | connector-cause |
| consequently | en consecuencia | Costs rose and, consequently, profits fell. | connector-cause |
| this leads to | esto provoca | Pollution leads to health problems. | connector-cause |
| however | sin embargo | The plan is costly; however, it is necessary. | connector-contrast |
| nevertheless | no obstante | It is risky; nevertheless, it is worth trying. | connector-contrast |
| whereas | mientras que | Cities are busy, whereas villages are calm. | connector-contrast |
| despite | a pesar de (+ sustantivo / -ing) | Despite the cost, the project continued. | connector-contrast |
| although | aunque (+ oración) | Although cars are convenient, they pollute. | connector-contrast |
| moreover | además | The plan is cheap; moreover, it is effective. | connector-addition |
| furthermore | además / es más | Furthermore, it creates jobs. | connector-addition |
| for instance | por ejemplo | Many cities, for instance Tokyo, are crowded. | connector-example |
| to illustrate | para ilustrar | To illustrate, consider renewable energy. | connector-example |
| in conclusion | en conclusión | In conclusion, the benefits outweigh the drawbacks. | connector-conclusion |
| on balance | en conjunto / sopesándolo | On balance, the policy is beneficial. | connector-conclusion |

---

# MAZO 3 — COLOCACIONES CON VERBOS ACADÉMICOS
| en | es | example | topic |
|---|---|---|---|
| conduct research | realizar una investigación | Scientists conduct research on climate. | collocation |
| address an issue | abordar un asunto | The report addresses this issue. | collocation |
| tackle a problem | abordar un problema | Governments must tackle this problem. | collocation |
| implement a policy | aplicar una política | The city implemented a new policy. | collocation |
| mitigate the impact | mitigar el impacto | Measures can mitigate the impact of floods. | collocation |
| raise awareness | concienciar | Campaigns raise awareness of recycling. | collocation |
| pose a threat | suponer una amenaza | Pollution poses a threat to health. | collocation |
| play a crucial role | desempeñar un papel crucial | Education plays a crucial role in development. | collocation |
| have a significant impact on | tener un impacto significativo en | Technology has a significant impact on jobs. | collocation |
| meet the demand | satisfacer la demanda | Supply struggles to meet the demand. | collocation |
| foster development | fomentar el desarrollo | Trade fosters economic development. | collocation |
| allocate resources | asignar recursos | The state allocates resources to schools. | collocation |
| make a contribution to | contribuir a | Volunteers make a contribution to society. | collocation |
| impose restrictions | imponer restricciones | The government imposed restrictions on traffic. | collocation |
| gain access to | obtener acceso a | Students gain access to online libraries. | collocation |
| place emphasis on | poner énfasis en | The curriculum places emphasis on science. | collocation |
| reach a conclusion | llegar a una conclusión | The study reached a clear conclusion. | collocation |
| make a mistake | cometer un error | Beginners often make mistakes. | collocation |

---

# MAZO 4 — LENGUAJE DE TENDENCIAS (Writing Task 1)
| en | type | es | example |
|---|---|---|---|
| rise | verb | subir / aumentar | Prices rose steadily. |
| increase | verb | aumentar | Sales increased over the decade. |
| surge | verb | dispararse (al alza) | Demand surged in summer. |
| soar | verb | dispararse / remontar | Costs soared unexpectedly. |
| fall | verb | caer / bajar | Numbers fell slightly. |
| decline | verb | descender | Output declined gradually. |
| plummet | verb | desplomarse | Profits plummeted in 2020. |
| plateau | verb | estabilizarse (tras subir) | Sales plateaued after June. |
| level off | verb | estabilizarse | Prices levelled off in spring. |
| fluctuate | verb | fluctuar | Figures fluctuated all year. |
| a sharp rise | noun | una subida pronunciada | There was a sharp rise in demand. |
| a gradual decline | noun | un descenso gradual | The graph shows a gradual decline. |
| a peak | noun | un pico / máximo | Sales reached a peak in July. |
| sharply | adverb | de forma pronunciada | Prices rose sharply. |
| gradually | adverb | gradualmente | Numbers fell gradually. |
| significantly | adverb | significativamente | Output grew significantly. |
| slightly | adverb | ligeramente | Demand dropped slightly. |

---

# MAZO 5 — UPGRADES (básico → Band 7+)
| basic | upgrades | note |
|---|---|---|
| good | beneficial / advantageous / positive | Úsalo según contexto; no fuerces. |
| bad | detrimental / harmful / adverse | "harmful TO", "detrimental TO". |
| big | significant / substantial / considerable | Para cantidades o efectos. |
| small | slight / marginal / minimal | Para cambios pequeños. |
| important | crucial / vital / essential / pivotal | "Pivotal" mal usado baja la nota. |
| many | numerous / a significant proportion of | Evita repetir "a lot of". |
| problem | issue / challenge / concern | Más formal y preciso. |
| thing | factor / aspect / element | "Thing" es vago; evítalo en Writing. |
| get | obtain / acquire / gain | "gain access", "acquire skills". |
| help | facilitate / assist / aid | Registro académico. |
| show | demonstrate / illustrate / reveal | Para datos y gráficos. |
| think | believe / maintain / contend | Varía tus verbos de opinión. |
| because of | due to / owing to / as a result of | + sustantivo. |
| nowadays | currently / in contemporary society | Evita empezar siempre con "nowadays". |

---

# MAZO 6 — GRAMÁTICA (conceptos)
| concept | rule_es | example_en | tag |
|---|---|---|---|
| Present simple | Hechos, rutinas, verdades. Sujeto + verbo (+ -s en 3ª persona). | Water boils at 100 degrees. | tenses |
| Present continuous | Acción en curso ahora o tendencia actual: am/is/are + -ing. | More people are working from home. | tenses |
| Present perfect | Pasado con relevancia presente, o con since/for: have/has + participio. | Technology has transformed education. | present-perfect |
| Present perfect vs past simple | Tiempo terminado o específico = past simple; con since/for o sin tiempo concreto = present perfect. | I went to Japan in 2019. I have lived here for five years. | present-perfect |
| Present perfect continuous | Acción que sigue, con énfasis en duración: have/has been + -ing. | Pollution levels have been rising. | tenses |
| Past simple | Acción terminada en momento pasado concreto: verbo + -ed o irregular. | The government introduced a policy in 2020. | tenses |
| Past continuous | Acción en progreso en el pasado: was/were + -ing. | I was studying when the power went out. | tenses |
| Past perfect | Acción anterior a otra acción pasada: had + participio. | By 2010, the population had doubled. | tenses |
| Future will | Predicciones y decisiones espontáneas: will + infinitivo. | Automation will change the workforce. | tenses |
| Future going to | Planes e intenciones, o predicción con evidencia. | The number is going to rise. | tenses |
| Future perfect | Acción terminada antes de un punto futuro: will have + participio. | By 2030, the city will have built three lines. | tenses |
| Modal verbs (forma) | Modal + infinitivo sin "to"; no cambian en 3ª persona. | She can swim. (NO "she cans") | modals |
| Modal must vs have to | must = obligación interna/fuerte; have to = obligación externa. | Governments must act. I have to renew my visa. | modals |
| Modal should | Consejo o recomendación: should + infinitivo. | Schools should teach financial literacy. | modals |
| Deduction present | must be (seguro), might/may/could be (posible), can't be (imposible). | He must be tired. That can't be true. | modals |
| Deduction past | must have / might have / can't have + participio. | The thief must have had a key. | modals |
| should have done | Algo que debió hacerse y no se hizo. | The government should have acted sooner. | modals |
| Zero conditional | Verdades generales: If + present, present. | If you heat ice, it melts. | conditionals |
| First conditional | Futuro probable: If + present, will + infinitivo. | If we invest in education, literacy will improve. | conditionals |
| Second conditional | Hipotético presente/futuro: If + past simple, would + infinitivo. | If I were the minister, I would reform the system. | conditionals |
| Third conditional | Pasado irreal: If + past perfect, would have + participio. | If they had acted earlier, the disaster would have been avoided. | conditionals |
| Conditional rule | Nunca "will" ni "would" en la cláusula con "if". | If I go (NO "if I will go"), I will tell you. | conditionals |
| Passive voice | be (en el tiempo) + participio; cuando la acción importa más que el agente. | The law was passed in 2020. | passive |
| Passive for process | Procesos artificiales en Task 1: present simple passive. | The beans are harvested and then dried. | passive |
| Defining relative clause | Información esencial, sin comas: who/which/that. | The students who study hard succeed. | relative-clauses |
| Non-defining relative clause | Información extra, con comas, sin "that". | London, which is the capital, is expensive. | relative-clauses |
| Reduced relative clause | Se omite pronombre + be para condensar. | The measures introduced last year worked. | relative-clauses |
| Complex sentence | Cláusula principal + subordinada para sonar Band 7. | Although cars are convenient, they pollute, which is why regulation is needed. | complex-sentences |
| despite vs although | despite/in spite of + sustantivo o -ing; although + oración. | Despite the rain... / Although it was raining... | complex-sentences |
| Article a/an | Contable singular no específico; en inglés sí se usa. | She is an architect. | articles |
| Article the | Algo específico o ya mencionado. | The policy introduced last year. | articles |
| Zero article (general) | Generalizaciones e incontables en sentido general: sin "the". | Life is hard. Technology has changed society. | articles |
| Uncountable nouns | information, advice, research: sin a/an ni plural. | a piece of information (NO "an information") | countable |
| much vs many | much + incontable; many + contable plural. | much money, many people | countable |
| few vs little | few + contable; little + incontable. | few jobs, little time | countable |
| Subject-verb: people | "people" es plural. | People are waiting. | agreement |
| Subject-verb: everybody | everybody/everyone/each son singulares. | Everybody is welcome. | agreement |
| a number of vs the number of | "a number of" + plural; "the number of" + singular. | A number of factors contribute. The number of cars has risen. | agreement |
| Gerund verbs | enjoy, avoid, suggest, consider + -ing. | They suggested building more schools. | gerund-infinitive |
| Infinitive verbs | want, decide, hope, plan + to + infinitivo. | The government decided to invest. | gerund-infinitive |
| Preposition + -ing | Tras preposición siempre -ing. | interested in learning (NO "in to learn") | gerund-infinitive |
| Comparatives | 1 sílaba + -er; 3+ sílabas more; than en la comparación. | cheaper than; more expensive than | comparatives |
| Superlatives | the + -est o the most. | the cheapest; the most important | comparatives |
| Word order | Sujeto + Verbo + Objeto; adjetivo antes del sustantivo. | a serious problem (NO "a problem serious") | word-order |
| No omitir sujeto | El inglés exige sujeto; usa "it" o "there". | It is important. There are many factors. | word-order |
| Comma splice | No unir dos oraciones con coma sola; usa punto, ; o conector. | Pollution is rising; it is a serious problem. | punctuation |

---

# MAZO 7 — ERRORES TÍPICOS DE HISPANOHABLANTES (corrección)
| wrong | right | why_es |
|---|---|---|
| I am agree | I agree | "agree" es verbo, no adjetivo; no lleva "to be". |
| The people is waiting | People are waiting | "people" es plural. |
| Depend of | Depend on | preposición fija. |
| I am here since morning | I have been here since morning | "since" exige present perfect. |
| The life is hard | Life is hard | generalización: artículo cero, sin "the". |
| The technology changed society | Technology changed society | generalización: sin "the". |
| I have 25 years | I am 25 years old | la edad se expresa con "be". |
| She is architect | She is an architect | contable singular necesita a/an. |
| An information | A piece of information | "information" es incontable. |
| Informations | Information | los incontables no tienen plural. |
| Despite it was raining | Despite the rain | "despite" + sustantivo, no + oración. |
| If I will go | If I go | no "will" tras "if". |
| Explain me | Explain to me | "explain" va con "to". |
| Listen me | Listen to me | "listen" va con "to". |
| A problem serious | A serious problem | el adjetivo va antes del sustantivo. |
| I am boring | I am bored | -ed = cómo te sientes; -ing = cómo es la cosa. |
| The lesson is bored | The lesson is boring | -ing describe la cosa que causa el sentimiento. |
| How is it called? | What is it called? | se usa "what", no "how". |
| Is important to study | It is important to study | no omitir el sujeto: usa "it". |
| Exist many factors | There are many factors | existencia con "there is/are". |
| They would have buy it | They would have bought it | participio tras "would have". |
| I have visited Paris last year | I visited Paris last year | tiempo terminado = past simple. |
| He live in Madrid | He lives in Madrid | 3ª persona singular lleva -s. |
| I have not seen nobody | I have not seen anybody | el inglés evita la doble negación. |
| Make research | Conduct research | colocación correcta. |
| Strong rain | Heavy rain | colocación correcta. |

---

## Resumen de mazos (para la app)
- M1 Vocabulario por tema (13 tags) — bidireccional.
- M2 Frases académicas (opinión, acuerdo, conectores).
- M3 Colocaciones con verbos académicos.
- M4 Lenguaje de tendencias Task 1.
- M5 Upgrades básico → Band 7+.
- M6 Gramática (conceptos) — recomendado en formato cloze.
- M7 Errores de hispanohablante (corrección) — máxima prioridad en la cola de repaso.
