<style lang="stylus" scoped>
    textarea
        width: 100%
</style>

<template lang="pug">
    #app
        p Digite no campo abaixo. Use: 
        ul
            li #[b *] para negrito;
            li #[b _] para sublinhado;
            li #[b ~] para italico;
            li #[b -] para cortar o texto.
            
        p Digite o caractere especial uma vez ao redor do texto para afetar mais de uma palavra (ex.: normal *negrito negrigo* normal) ou duas vezes antes da palavra que quer decorar (ex.: **negrito normal).
        
        textarea(rows="5" v-model="texto" @keyup="formatarTexto")
        br
        div(v-html="textoFormatado")
</template>

<script>
    export default {
        name: 'Editor',
        data: function () {
            return {texto: '', textoFormatado: ''}
        },
        methods: {formatarTexto}
    }

    const formatacoes = [
        ['*', 'b'],
        ['_', 'u'],
        ['-', 's'],
        ['~', 'i']
    ];

    function formatarTexto () {
        const fnReduce = (texto, [flag, tag]) => {
            return flagToTag({texto, flag, tag});
        };
        
        this.textoFormatado = formatacoes
            .reduce(fnReduce, this.texto)
            .replace(/\n([^\n]*)/, '<p>$1</p>');
    }

    function flagToTag ({texto, flag, tag}) {
        const formato = `<${tag}>$1</${tag}>`;
        const seletores = [
            `\\${flag}\\${flag}([^\\ ]*)`,
            `\\${flag}(.*)\\${flag}`
        ].map(s => new RegExp(s, 'g'));

        return texto
            .replace(seletores[0], formato + ' ')
            .replace(seletores[1], formato);
    }
</script>
