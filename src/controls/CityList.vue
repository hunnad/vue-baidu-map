<script>
import commonMixin from '@/base/mixins/common.js'

export default {
  name: 'bm-city-list',
  render () {},
  mixins: [commonMixin('control')],
  props: {
    anchor: {
      type: String
    },
    offset: {
      type: Object
    }
  },
  watch: {
    anchor () {
      this.reload()
    },
    offset () {
      this.reload()
    }
  },
  methods: {
    load () {
      const {BMap, map} = this
      const instance = this
      this.originInstance = new BMap.CityListControl({
        anchor: global[this.anchor],
        offset: this.offset,
        onChangeBefore () {
          instance.$emit('changeBefore')
        },
        onChangeAfter () {
          instance.$emit('changeAfter')
        }
      })
      map.addControl(this.originInstance)
    }
  }
}
</script>
