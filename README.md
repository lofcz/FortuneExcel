<p align="center">
  <img align="center" src="fortuneExcelLogo.png" width="150px" height="150px" />
</p>
<h1 align="center">FortuneExcel</h1>
<p align="center">FortuneExcel is an .xlsx and .csv import/export plugin for FortuneSheet / ProsperaSheet.</p>

<div align="center">

<p>
  <a href="https://www.npmjs.com/package/@lofcz/fortune-excel" alt="fortuneExcel on npm">
    <img src="https://img.shields.io/npm/v/@lofcz/fortune-excel" />
  </a>
  <a href="https://www.npmjs.com/package/@lofcz/fortune-excel" alt="fortuneExcel downloads">
    <img src="https://img.shields.io/npm/d18m/%40lofcz%2Ffortune-excel" />
  </a>
</p>

</div>

Fork of [`@corbe30/fortune-excel`](https://github.com/Corbe30/FortuneExcel) with Bun tooling, trusted npm provenance publishing, and merged improvements from [jlsi/FortuneExcel](https://github.com/jlsi/FortuneExcel) (Excel date display formatting, drawing/chart/shape import).

## Usage

1. Install the package:
    ```js
    bun add @lofcz/fortune-excel
    # or: npm i @lofcz/fortune-excel
    ```

2. Import/export toolbar item ([code example](https://github.com/lofcz/FortuneExcel/tree/main/src/stories/Plugin.tsx))
    > Note: `<FortuneExcelHelper />` is a hidden component.
    ```js
    import { FortuneExcelHelper, importToolBarItem, exportToolBarItem } from "@lofcz/fortune-excel";

    function App() {
      const sheetRef = useRef();
      const [key, setKey] = useState(0);
      const [sheets, setSheets] = useState(data);

      return (
        <>
          <FortuneExcelHelper
            setKey={setKey}
            setSheets={setSheets}
            sheetRef={sheetRef}
            config={{ // default = all values are true
              import: { xlsx: true, csv: true },
              export: { xlsx: true, csv: true },
            }}
          />
          <Workbook
            key={key} data={sheets} ref={sheetRef}
            customToolbarItems={[importToolBarItem(), exportToolBarItem()]}
          />
        </>
      );
    }
    ```

3. Programmatic import/export ([code example](https://github.com/lofcz/FortuneExcel/tree/main/src/stories/Manual.tsx))
    ```js
    import { transformFortuneToExcel } from "@lofcz/fortune-excel";

    const manualExport = async () => {
      const exportedFile = await transformFortuneToExcel(
        sheetRef,
        "xlsx", // or "csv"; default = "xlsx"
        true // start automatic download; default = true
      );
      console.log("Exported file data:", exportedFile);
    };

    <button onClick={manualExport}>Export</button>
    ```
    ```js
    import { transformExcelToFortune } from "@lofcz/fortune-excel";

    const manualImport = async (event) => {
      await transformExcelToFortune(
        event.target.files[0], // file type (csv/xlsx) is automatically identified
        setSheets,
        setKey,
        sheetRef
      )
    }
    ```

## Authors and acknowledgment

- [@Corbe30](https://github.com/Corbe30) — upstream FortuneExcel
- [@jlsi](https://github.com/jlsi) — date formatting + drawing object import
- [@midship-dev](https://github.com/midship-dev) — oneCellAnchor / absolute path / `ns2:embed` image fixes
- [@lofcz](https://github.com/lofcz) — this fork

Developers of [FortuneSheetExcel](https://github.com/zenmrp/FortuneSheetExcel):
- [@wbfsa](https://github.com/wbfsa)
- [@wpxp123456](https://github.com/wpxp123456)
- [@Dushusir](https://github.com/Dushusir)
- [@xxxDeveloper](https://github.com/xxxDeveloper)
- [@mengshukeji](https://github.com/mengshukeji)

Export support:
- [Orleans9](https://blog.csdn.net/zinchliang) - [article](https://blog.csdn.net/zinchliang/article/details/120262185)

## Contribution

1. Install [Bun](https://bun.sh)
2. `bun install`
3. `bun run prepare`
4. `bun run storybook`

## License

[MIT](http://opensource.org/licenses/MIT)
